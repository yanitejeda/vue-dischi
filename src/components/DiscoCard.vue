<template>
    <div class="card bnone ">
        <img :src="poster" class="card-img-top" alt="disco.title">
        <div class="card-body cardBg">

            <h3 class="card-title tittleColor">{{title}}</h3>
            <p class="card-text textColor ">
                <span>
                    {{author}} <br> 
                    {{year}} 
                </span>
            </p>
        </div>
     </div>
</template>

<script>
/* import DiscContainer from './DiscContainer.vue' */

export default {
    name:"DiscoCard",
    props:[
        'author','genre','poster','title','year'
    ]
}
</script>