<!-- This component takes in user input and passes it back to App.vue -->
<script>

export default {
    props: ['text', 'pages', 'years'],
    emits: ['update:text', 'update:pages', 'update:years'],
}

</script>

<template>
    
    <div class="columns">
        <div class="column">

            <div class="field">
                <div class="control has-icons-left">
                    <!-- Sends the input bar to the parent component -->
                    <input class="input" type="text" placeholder="Find a book" 
                    :value="text"
                    @input="$emit('update:text', $event.target.value)"/>
                    <span class="icon is-small is-left">
                        <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
                    </span>
                </div>
            </div>
            
            <div class="select is-info"
            :value="pages"
            @input="$emit('update:pages', $event.target.value)">
            <select>
                <option>All Lengths</option>
                <option>Less than 200 pages</option>
                    <option>200 to 400 pages</option>
                    <option>Greater than 400 pages</option>
                </select>
            </div>
            
            <div class="control"
            :value="years"
            @input="$emit('update:years', $event.target.value)">
            <label class="radio">
                <input type="radio" name="answer" value="all" checked>
                All Years
                </label>
                <label class="radio">
                    <input type="radio" name="answer" value="before">
                    Before 1900
                </label>
                <label class="radio">
                    <input type="radio" name="answer" value="after">
                    After 1900
                </label>
            </div>
            
        </div>
    </div>

</template>

<style>
</style>