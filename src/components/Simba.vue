<template>
    <div>
        <h2>Hello {{name}} </h2>
        <ul>
            <li>Age {{age}} </li>
            <li>Color {{color}} </li>
            <li>{{treat}} </li>
        </ul>
    </div>
</template>
<script>
export default {
    props: ["treat"],
    data: function() {
        return {
            name: 'Simba',
            age: 6,
            color: "Black"
        };
    }
};
</script>
<style lang="scss">
    h2 {
        color: coral
    }
</style>
