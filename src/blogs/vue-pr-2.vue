<template>
  <article>
    <h2>Before</h2>
    <p>The last article talked about the MVVM pattern, which led to the data hijacking of vue.</p>
    <h2>Data hijacking</h2>
    <h3>What is data hijacking?</h3>
    <p>
      <span style="color:lightgreen"> Read and modify interception of properties.</span>
      In short, any changes in data must be monitored, so that corresponding operations can be made according to data
      changes.Without data hijacking, there is no way to update the data without knowing the state of the data.
    </p>
    <h3>how does it work in vue?</h3>
    <p>The method of data hijacking is different in vue2 and vue3.</p>
    <h4>Vue2 --- Object.defineProperty </h4>
    <p>The static method Object.defineProperty() defines a new property directly on an object, or modifies an existing
      property on an object, and returns the object. You can learn more on <a style="color:lightblue" target="_blank"
        href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty">MDN</a>.
    </p>
    <p>
    <pre v-html="example"></pre>
    </p>
    <p>
      As shown above, I define an object 'o', then it has a property 'a',When i get the property normally,it print 1
      what i defined.And i use defineProperty, define its getter and setter, when i get the property again, The printed
      data is different.what it prints was the return value in getter.And change 'a', found that it called the setter.
      Again, it printed the return value in getter.
    </p>
    <p>
      Therefore, use getter and setter to data reactivity.However, this approach has many flaws.
    <ul>
      <li>
        Unable to monitor property modification and deletion;
      </li>
      <li>
        Some changes to the array cannot be monitored either;
      </li>
      <span style="color: lightpink">obj: {{ obj }}</span>
      <q-btn @click="changeObj" color="primary" style="margin-left: 10px">change Object</q-btn>
    </ul>
    see the example above, This button is used to delete the A property in the object and add a C property. The
    results in vue2 and vue3 are different.This blog is based on 3, so the result is the result of vue3. If you want to
    know
    the result of vue2, you can build a demo to try it yourself.
    The way to listen to arrays in vue2 is to rewrite some array methods.For example, There is a push method on the
    prototype of Array, There is a push method on the prototype of Array. We rewrite this push method. The final
    function is still to add a data to the array. However, we can add our responsive method to it, and then feed it back
    to the webpage.Does that apply to all scenarios? Of course not！when you change the array like 'arr = []' or
    'arr.length = 2',what should you do?
    </p>
    <h4>Vue3 --- Proxy, Reflect </h4>
    <p>Based on some problems in vue2, there is another way to implement Reactivity in vue3.</p>
    <p>
      The <a style="color:lightblue" target="_blank"
        href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy">Proxy</a>
      object enables you to create a proxy for another object, which can intercept and redefine fundamental
      operations for that object.This definition is in MDN. the same to above, if you want to learn more, MDN can help
      you.
    </p>
    <p>
    <pre v-html="example2"></pre>
    </p>
    <p>
      If you have used vue3, you should know that ref and reactive are required to implement data Reactivity.
      Let's see what the reactive method looks like in the vue source code(Based on version 3.2.27,
      reactivity/src/reactive.ts):
    </p>
    <p>
      <q-img src="../assets/vue/reactive1.png" />
    </p>
    <p>
      <q-img src="../assets/vue/reactive2.png" />
    </p>
    <p>
      Remove some basic judgments
    </p>
    <p>
      <q-img src="../assets/vue/reactive3.png" />
    </p>
    <p>
      As shown above, The reactive function returns a Proxy object, in this Object, What is this handler method used
      for? In the above example, the handler function in proxyPerson has a get method, in vue , The key logic processing
      is here.Different target has different handler, The above collectionHandlers and baseHandlers are part of it, You
      can also find collectionHandlers from the source code to handler complex object like Map, Set, WeakMap,
      WeakSet. Array and Object were baseHandlers.
    </p>
    <p>What are they works?</p>
    <p>
      Let's take baseHandlers as an example(reactivity/src/baseHandlers.ts):
    </p>
    <p>
      <q-img src="../assets/vue/handler1.png" />
    </p>
    <p>
      <q-img src="../assets/vue/handler2.png" />
    </p>
    <p>
      Define a reactive Object and log it. This handler object is presented in front of you.Because the space is too
      long, the content related to the handler is placed in the next content.
    </p>
    <p>
      Thanks for reading!
    </p>
  </article>
</template>

<script lang='ts'>
import { defineComponent, reactive } from "vue";
import Prism from 'prismjs';
export default defineComponent({

  setup() {
    const obj = reactive({
      a: 1,
    })
    const changeObj = () => {
      delete obj.a;
      obj.c = 5
    }
    const code =
      `let o = {
  a: 1
};
console.log(o.a)
Object.defineProperty(o, 'a', {
  get () {
    console.log('get value')
    return 2
  },
  set (v) {
    console.log('set value ', v)
  }
})
console.log(o.a)
o.a = 5
console.log(o.a)`;
    const code2 =
      `const person = {
  name: 'Jinwen Wu',
  age: 27
}

const proxyPerson = new Proxy(person,{
  get: function(target, propKey) {
    return 100
  }
})

console.log(person.name)  // Jinwen Wu
console.log(proxyPerson.name)  // 100
console.log(proxyPerson.age) // 100`
    const example = Prism.highlight(code, Prism.languages.javascript, 'javascript')
    const example2 = Prism.highlight(code2, Prism.languages.javascript, 'javascript')
    console.log(obj)
    return {
      obj,
      example,
      example2,
      changeObj
    };
  },
});
</script>

<style scoped lang='scss'>
.q-img {
  max-width: 600px;
}
</style>