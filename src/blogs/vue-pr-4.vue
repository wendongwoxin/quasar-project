<template>
    <article>
        <h2>Reactivity</h2>
        <p>In the previous articles, we talked about the related content of Proxy and Reflect, today we are talking
            about the reactivity of vue3.So,what is the reactivity?</p>
        <p>
            price: <input v-model="price" type="number" />
            quantity: <input v-model="quantity" type="number" />
            total: {{ total }}
        </p>
        <p>As shown above, if we change the input value, the result changed.We use computed to calculate the result and
            Dynamic update.But how did it do it?</p>
        <h3>Track, Trigger and Effect</h3>
        <p>Before we dive into it, let's understand three concepts:
        <ul>
            <li>effect: After a responsive object property or itself changes, the impact on other individuals</li>
            <li>track: Tracking is the constant recording of the side effects of a reactive object property</li>
            <li>trigger: When an object itself/property changes, we need to trigger all the effects of the previous
                track</li>
        </ul>
        </p>
        <p>Next, let's see how to use these methods to do it?</p>
        <p>
            <q-img src="../assets/vue/reactivity_1.png" />
        </p>
        <p>see above!when i define a reactive object, then we use Proxy, and in getter methods we use track and add the
            effects about this object, in setter methods we use trigger to execute the effects functions, Similar to the
            following code:</p>
        <p>
            <q-img src="../assets/vue/reactivity_2.png" />
        </p>
        <p>
            The above content is aimed at an object, a scene, but In fact, the demand is far more than that. How to
            achieve it in the vue source code, let's go step by step.
        </p>
        <p>
            <q-img src="../assets/vue/reactivity_3.png" />
        </p>
        <p>
            See above, in the vue source code, Define a WeakMap named targetMap to store effects between different
            targets.First we need to create a reactive effect for rendering (activeEffect in the image below), this is
            not created in the effect.ts, but
            in runtime-core/src/renderer.ts, if you want to know anymore about this, you can learn from the source code.
            Then track it!
        </p>
        <p>
            <q-img src="../assets/vue/track.png" />
        </p>
        <p>
            How to Trigger?
        </p>
        <p>
            <q-img src="../assets/vue/trigger.png" />
        </p>
        <p>
            After a long time of study, we finally talked about the principle of vue reactivity in a
            short way. There are many difficulties for me, so many places may not be
            detailed enough, but in the process I learned a lot and also learned some source code knowledge,which is a
            rare learning opportunity.
        </p>
        <p>
            Next, we will continue to explore other principle knowledge of vue3, and finally thank you for reading!
        </p>
    </article>
</template>

<script lang='ts'>
import { defineComponent, computed } from 'vue';
import { ref } from 'vue';

export default defineComponent({
    setup() {
        const price = ref(0);
        const quantity = ref(0);
        const total = computed(() => {
            return price.value * quantity.value
        })
        return {
            price,
            quantity,
            total
        };
    },
});
</script>

<style scoped lang='scss'>
.q-img {
    max-width: 600px;
}
</style>