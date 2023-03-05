<template>
    <div class="projectsdetails">
        <div v-if="project">
            <!-- {{ project }} -->
            <h1 class="title-color">{{ project.name }}</h1>
            <br>
            <div class="back-button"><a @click="$router.go(-1)">Retour</a></div>
            <br>
            <h2 class="type-color">Type : {{ project.project_type.type }}</h2>
            <br>
            <div class="techcontainer">
                <div v-for="tech in project.technologies" :key="tech.id">
                    <div class="techimgcontainer">
                        <img :src="tech.techimg.url" alt="" width="50">
                    </div>
                </div>  
            </div>
            <br>
            <div class="projectimgcontainer">
                <img class="projectimg" :src="project.image.url" alt="">
            </div>
            <br>
            <p class="project-text">{{ project.description }}</p>
        </div>
    </div>
</template>

<script setup>

    const { findOne } = useStrapi()
    const route = useRoute()
    const project = ref()

    onMounted( async() => {
        project.value = await findOne(`projets?filters[slug]=${route.params.slug}&populate=deep`)
        project.value = project.value.data[0]
        
    })
</script>

<style>

.back-button {
    background-color: rgb(171, 216, 255);
    width: fit-content;
    padding: 10px;
    margin-left: 20px;
    border-radius: 5px;
}

.project-text {
    color: rgb(171, 216, 255);
    font-weight: 300;
    letter-spacing: 1px;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
    padding: 20px;
    background-color: rgb(71, 71, 71);
}

.projectimgcontainer {
    width: 40%;
    margin: auto;
}

.projectimg {
    width: 100%;
    margin: auto;
}


.techcontainer {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 50px;
}

.project-text {
    margin: auto;
    width: 40%;
}

.projectsdetails  {
    background-color: rgb(44, 43, 43);
    height: 100vh;
}

.title-color {
    color: rgb(52, 99, 253);
    margin: auto;
    text-align: center;
}

.type-color {
    margin: auto;
    text-align: center;
    color: rgb(171, 216, 255);
}

</style>
