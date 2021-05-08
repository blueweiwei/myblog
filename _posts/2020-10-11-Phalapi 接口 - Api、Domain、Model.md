---
layout: post
title: Phalapi 接口 - Api、Domain、Model
date: 2020-10-11
Author: 小萌 
tags: [php接口]
comments: true
toc: true


---



>  接触到了phalapi框架，学习到了三层之间有着密不可分的关系，记录一下

### 首先

看一下官方的讲解：

![img](https://i.loli.net/2020/10/11/QvrgsuIO1BG45wk.png)

##### Api接口服务层应该做：

- 应该：对用户登录态进行必要的检测
- 应该：控制业务场景的主流程，创建领域业务实例，并进行调用
- 应该：进行必要的日记纪录
- 应该：返回接口结果
- 应该：调度领域业务层

##### Domain领域业务层应该做：

- 应该：体现特定领域的业务规则
- 应该：对数据进行逻辑上的处理
- 应该：调度数据模型层或其他领域业务层

##### Model数据模型层应该：

- 应该：进行数据库的操作
- 应该：实现缓存机制

不要跨层进行调用，因为这样会加大代码量！！！

### 解剖三层之间的关系

真正看懂Phalapi官方的话，那么一定会对分离与分层感触很深了。

下面直接看看一个功能下的三层之间应当如何管理。

##### Api层 注册代码

```php
<?php
namespace App\Api\User;
/** app/api/user/user.php  **/

use PhalApi\Api;
use App\Domain\User\User as UserDomain;
use PhalApi\Exception\BadRequestException;

class User extends Api {
    
    /**
     * 注册账号
     * @desc 注册一个新账号
     * @return int user_id 新账号的ID
     */
    public function register() {
        $domain = new UserDomain();
        $user = $domain->getUserByUsername($this->username, 'id');
        if ($user) {
            throw new BadRequestException($this->username . '账号已注册');
        }
        
        $moreInfo = array(
            'avatar' => $this->avatar,
            'sex' => $this->sex,
            'email' => $this->email,
            'mobile' => $this->mobile,
        );
        $userId = $domain->register($this->username, $this->password, $moreInfo);
        
        return array('user_id' => $userId);
    }
}
```

##### Domain层 注册代码

```php
<?php
namespace App\Domain\User;
/** app/domain/user/user.php **/

use App\Model\User\User as UserModel;

class User {
    /**
     * 注册新用户
     *
     * @param string $username 账号
     * @param string $password 密码
     * @param array $moreInfo 更多注册信息，必须在数据库表中有此字段
     * @return int 用户id
     */
    public function register($username, $password, $moreInfo = array()) {
        $newUserInfo = $moreInfo;
        $newUserInfo['username'] = $username;

        $newUserInfo['salt'] = \PhalApi\Tool::createRandStr(32);
        $newUserInfo['password'] = $this->encryptPassword($password, $newUserInfo['salt']);
        $newUserInfo['reg_time'] = $_SERVER['REQUEST_TIME'];

        $userModel = new UserModel();
        $id = $userModel->insert($newUserInfo);
        
        return intval($id);
    }
}
```

##### Model层 注册代码

```php
<?php
namespace App\Model\User;
/** app/model/user/user.php **/

use PhalApi\Model\DataModel;
class User extends DataModel {
    protected function getTableName($id) {
        return 'phalapi_user';
    }

    public function getInfo($userId) {
        return $this->getORM()->select('*')->where('id = ?', $userId)->fetch();
    }

    /**
     * 批量获取用户快照，并进行反转，以便外部查找
     */
    public function getSnapshotByUserIds(array $userIds)
    {
        $rs = array();
        if (empty($userIds)) {
            return $rs;
        }

        $rows =self::getORM()
            ->select('id,nickname,avatar')
            ->where('id', $userIds)
            ->fetchAll();

        foreach ($rows as $row) {
            $rs[$row['id']] = $row;
        }

        return $rows;
    }
}
```



### 结束