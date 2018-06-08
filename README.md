# VueOver
1、引入jquery
<script src="/assets/js/jquery-3.3.1.min.js"></script>
2、只有在updated和mounted后才能使用jquery，否则jquery找不到dom

3、通过jquery为div赋值
mounted:function(){
                $("#app").html("我是jquery~！")
            }
4、在外部调用构造器内部的方法
 var vm = new Vue({
            el:'#app',
            data:{
                message:'hello world'
            },
            mounted:function(){
                $("#app").html("我是jquery~！")
            },
            methods:{
                add:function(){
                    console.log('调用了构造器内部的add方法');
                }
            }
        })

        vm.add();


























