---
layout: post
title: "php设计模式英雄联盟篇-单例模式"
date:   2015-07-29
subtitle: ""
author: "RryLee"
tags:
    - php
    - 设计模式
---

这里我们用英雄联盟的例子来看看单例模式的实现与应用

单例模式，总的来说就是该类只能有一个实例化对象。在 LOL 中可以这样理解，所有的英雄都有回城时间，技能数量，最高等级等一系列属性。我们在实例化其他英雄对象时，这些共同属性不需要继承自英雄这个父类，我们可以直接使用这个共有实例。

    class CommonPerproties
    {
        public static $backtime = 8;
        public static $skillNum = 3;
        public static $maxRank  = 18;
    }
    // 先有这么一个基础类，一步步完成我们的单例模式。
    $Anni = new CommonPerproties();
    $Wukong = new CommonPerproties();
    echo $Anni::$backtime; // 8
    echo $Wukong::$maxRank; // 18
    var_dump($Anni === $Wukong); // bool(false)

这两个对象不是同一个，不是我们想要的结果。

    class CommonPerproties
    {
        // 这里全部改为 private 属性，以防止子类修改
        private $backtime = 8;
        private $skillNum = 3;
        private $maxRank  = 18;

        // 该类的实例对象
        private static $instance;

<<<<<<< HEAD
        // 这里修改构造方法属性为 protected，表示该类不能通过 new 来实例化
=======
        // 这里修改构造方法属性为 private，表示该类不能通过 new 来实例化
>>>>>>> b0321639829991bff67c78ada25720756da720f3
        private function __construct()
        {

        }

        // 通过 getInstance 方法得到对象
        public function getInstance()
        {
            if (empty(self::$instance)) {
                self::$instance = new CommonPerproties();
            }

            return self::$instance;
        }

        public function getPerproty($name)
        {
            return $this->$name;
        }
    }
    $Anni = CommonPerproties::getInstance();
    $Wukong = CommonPerproties::getInstance();
    echo $Anni->getPerproty('backtime'); // 8
    echo $Wukong->getPerproty('skillNum'); // 3
    var_dump($Anni === $Wukong); // bool(true)

>这里我们拿到的安妮和猴子的实例指向同一个，那么完了吗，并没有

假设当对面红色方也选择了安妮，而且通过 clone 得到

    $RedAnni = clone $Anni;
    var_dump($Anni === $RedAnni); // bool(false)

这种做法是不允许的，所以我们需要禁止它

在代码中加上

    ...
    // 防止外部使用 clone 魔术方法
<<<<<<< HEAD
    pricate function __clone()
=======
    private function __clone()
>>>>>>> b0321639829991bff67c78ada25720756da720f3
    {
        # code...
    }

    /**
     * 把反序列化方法声明为 private，防止反序列化单例
     *
     * @return void
     */
    private function __wakeup()
    {
    }
    ...

最后，大功告成，未完。。。
