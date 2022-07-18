<template>
    <article>
        <h2>Handler</h2>
        <p>In the last article, we found that handler has methods like getter, setter, etc. How do they implement them?
        </p>
        <h3>Reflect</h3>
        <p>
            Before we discuss this handler, let's talk about Reflect, Reflect is a built-in object that provides methods
            for interceptable JavaScript operations.The most important is The Reflect object provides the following
            static functions which have the same names as the Proxy handler methods.This is why vue3 used Reflect.
            Let's take the getter method as an example,Please see the picture below:
        </p>
        <p class="row">
            <q-img src="../assets/vue/reflect1.png" />
        </p>
        <p>
            When i define two handler, and define an object person, use two different handlers,and the object person has
            a getter method.
        </p>
        <p>
            <q-img src="../assets/vue/reflect2.png" />
        </p>
        <p>
            And define two objects with __proto__ properties as reactive1 and reactive2, where the name is both Bob.Then
            we use their getter method,but the result is different. What's causing this? --- Reflect's receiver.In MDN,
            he defines it like this: <br>
        <ul>
            <li>
                The value of this provided for the call to target if a getter is encountered. When used with Proxy, it
                can be an object that inherits from target.
            </li>
        </ul>
        </p>
        <p>
            it can modify this in property access to point to the incoming receiver object.
        </p>
        <p>
            The above are just some of the functions of Reflect, there are more we can find out by looking at the
            documentation and practice.
        </p>
        <h3>getter</h3>
        <p>The getter method is similar to the getter in our previous article，It just adds some listeners for arrays,
            symbols and other objects, and track these.</p>
        <h3>setter?</h3>
        <p>Before i introduce the setter, i want to introduce some Reactivity API in vue3.Because it's hard to explain
            reactive principles without explaining these apis.</p>
        <p>This is the end of this article, thank you for reading.</p>
    </article>
</template>

<script lang='ts'>
import { defineComponent } from 'vue';

export default defineComponent({
    setup() {

        return {
        };
    },
});
</script>

<style scoped lang='scss'>
.q-img {
    max-width: 600px;
}
</style>