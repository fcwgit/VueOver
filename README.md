# VueOver

主要讲述实例事件


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

======================mount=============================
定义扩展
var jsPang = Vue.extend({
            template:`
                <p>{{message}}</p>
            `,
            data:function(){
                return {
                    message:'hello i am jspang'
                }
            },
            mounted:function(){
                console.log("mounted 被创建了");
            }
        });
挂载扩展
        var vm = new jsPang().$mount("#app ");

卸载
<p><button onclick="destroy()">destroy</button></p>
function destroy(){

            vm.$destroy();
        }

强制更新
<p><button onclick="forceUpdate()">forceUpdate</button></p>


function forceUpdate(){
            vm.$forceUpdate();
        }
function forceUpdate(){
            vm.message = 'hhhhhhhhhhh';
            vm.$forceUpdate();
        }

message被修改之后，钩子函数nextTick被调用
<p><button onclick="tick()">tick</button></p>
function tick(){
            vm.message = 'update message info';
            vm.$nextTick(function(){
                console.log('message 更新之后我被调用了');
            })
        }


======================构造器之外添加事件=============================

构造器外面新增事件
<button onclick="reduce()">reduce</button>

vm.$on('reduce',function(){
            console.log('执行了Reduce方法');
            this.num--;
        })

        function reduce(){
            vm.$emit('reduce');
        }

只执行一次的方法
<button onclick="reduceOnce()">reduceOnce</button>

vm.$once('reduceOnce',function(){
            console.log('只执行一次的方法');
            this.num--;
        })

        function reduceOnce(){
            vm.$emit('reduceOnce');
        }

注意：分为两步，第一步写入事件，第二步使用emit外面调用执行

关闭某一个事件
<button onclick="off()">off</button>
function off(){
            vm.$off('reduce');
        }


