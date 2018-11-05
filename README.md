# js-Inheritance-pattern
js的继承模式


共享模式： (好处：是可以几个函数可以共享一个原型，坏处：不能创建自己私有的原型)

               Prest.prototype.lasName="张三"
                function Prest(){         	
                 }

                function Son(){
                 }

              function inherit(son,prest){
               son.prototype=prest.prototype;
             }
                inherit(Son,Prest)

             var sons=new Son();
             sons.lasName     //张三

             var  prests=new Prest();
             prests.lasName   //张三




圣杯模式：  可以继承原型,也可以在自己的对象上创建私有的原型


                Prest.prototype.lasName="张三";
                
                 function Prest(){         	
                 }
                 function Son(){
                 }

                 function inherit(son,prest){
                   function F(){};
                   F.prototype=prest.prototype;
                   son.prototype=new F();
                 }
                 inherit(Son,Prest)

                 var sons=new Son();
                 Son.prototype.name="王五"
                  sons.lasName   //张三
                  sons.name       //王五


                 var prests=new Prest()

                    prests.lasName  //张三
                    prests.name    //undefined







