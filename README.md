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
                   son.prototype.constructor=son;    //把son的构造器指针 指向到了自己本身
                 }
                 inherit(Son,Prest)

                 var sons=new Son();
                 Son.prototype.name="王五"
                  sons.lasName   //张三
                  sons.name       //王五


                 var prests=new Prest()

                    prests.lasName  //张三
                    prests.name    //undefined



         以上继承模式都有副作用
         
            思考如下代码(推荐使用)
            
              Obj.prototype.getName=function(){
                  return this.name
               }
                 function Obj(name){
                    console.log(this)
                    this.name=name;
                 }
                  function Obj1(name,age){
                         Obj.call(this,name);
                         this.age=age;
                  }
                Obj1.prototype=Object.create(Obj.prototype);
                Obj1.prototype.getAge=function(){
                   return this.age;
                }
                //console.log(Obj1.prototype)
                var k=new Obj1("英男",25)
                  k.getName()  //英男
                  k.getAge()   //25

            
            
            



