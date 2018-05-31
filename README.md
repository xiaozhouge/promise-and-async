# promise-and-async
## 练习promise，下一个异步操作要用到上一个异步的结果
```javaScript
   const  p1=()=>{
        let p1_data;
        return new Promise((resolve,reject)=>{
          setTimeout(()=>{
            p1_data=1;
            console.log(p1_data)
            resolve(p1_data)
          },4000)
        })
      }
      const p2=(value)=>{
        return new Promise((resolve,reject)=>{
          setTimeout(()=>{
            value++;
            console.log(value)
            resolve(value)
          },2000)
        })
      }
      const p3=(value)=>{
        return new Promise((resolve,reject)=>{
          setTimeout(()=>{
            value++;
            console.log(value)
            resolve(value)
          },3000)
        })
      }
      
      p1().then((value)=>{
        return p2(value)
      })
      .then((value)=>{
        return p3(value)
      })
      .then((value)=>{
        console.log('终于等到你',value)
      })
```
## 然后用async语法糖进行封装
```javaScript
    const  p1=()=>{
        let p1_data;
        return new Promise((resolve,reject)=>{
          setTimeout(()=>{
            p1_data=1;
            console.log(p1_data)
            resolve(p1_data)
          },4000)
        })
      }
      const p2=(value)=>{
        return new Promise((resolve,reject)=>{
          setTimeout(()=>{
            value++;
            console.log(value)
            resolve(value)
          },2000)
        })
      }
      const p3=(value)=>{
        return new Promise((resolve,reject)=>{
          setTimeout(()=>{
            value++;
            console.log(value)
            resolve(value)
          },3000)
        })
      }
      
     const asyncPS = async function () {
        let f1=await p1()
        let f2=await p2(f1);
        let f3=await p3(f2);
        console.log('终于等到你',f3)
        return f3;
      };
      asyncPS();
```
