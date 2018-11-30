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

            
            
         自己写的玩的一个继承封装
         <div class='div'></div>
         
         function Parent(width,heigth,$elem){
            console.log(this)
                this.width=width;
                this.heigth=heigth;
                this.$elem=null;
          }

          Parent.prototype.implement=function($appendto){
            console.log(this)
            if(this.$elem){
              this.$elem.css({width:this.width+"px",height:this.heigth+"px"}).appendTo($appendto)
            }
          }

        function Son(zi_width,zi_heigth,lable){
             Parent.call(this,zi_width,zi_heigth);
             this.lable=lable;
             this.$elem=$("<button>").text(this.lable)
        }
        Son.prototype=Object.create(Parent.prototype);
        Son.prototype.implement=function(as){
             console.log(this)
             Parent.prototype.implement.call(this,as);
             this.$elem.click(function(){
               console.log("我是click事件")
               });
           }
        //   Son.prototype.onClick=function(s){
        //     console.log(this)
        //     console.log("我是click事件"+s)
        // }
           var div=$(".div")
           var a=new Son(190,100,"按钮")
           a.implement(div)

         
         
         
         
         
         
         
         
         



