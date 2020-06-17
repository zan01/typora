#### Vue 初始化过程

---

1. ##### 创建阶段

   > beforeCreate()

   ```
   data 和 methods 还没初始化
   ```

   >created()

   ```
   成功创建组件实例,不能访问模板
   ```

2. ##### 挂载阶段

   > beforeMount()

   ```
   将模板编译完成后,放入内存中
   ```

   > mounted()

   ```
   beforeMount()和mounted()两个方法执行之间,将内存中的模板渲染到真正的页面中去
   ```

3. ##### 更新阶段

   > beforeUpdate()

   ```
   此时,页面中的数据未更新,data中的数据已经更新
   ```

   > updated()

   ```
   beforeUpdate()和updated()之间完成页面数据的更新渲染
   ```

4. ##### 销毁阶段

   > beforeDestory()

   ```
   实例还可以正常使用,还没开始真正销毁
   ```

   > destory()

   ```
   销毁实例,都不可再用
   ```

   