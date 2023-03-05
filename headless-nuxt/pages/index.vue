<template>
    
    <div class="page-container">
        <div class="header-container">
            <header>
                <nav class="navwrapper">
                    <h1 class="logo">L</h1>
                    <ul class="navlinks">
                        <li><a href="#projets">Projets</a></li>
                        <li><a href="#contact">Contact</a></li>
                    </ul>
                </nav>
            </header>

            <div class="header-content">
                <p class="header-phrase">Bonjour, je suis</p>
                <br>
                <h1 class="header-title">Louis Chu</h1>
                <br>
                <h1 class="header-title">Je suis developpeur web</h1>
                <br>
                <p class="text">Bienvenue sur mon site web ! Ici, vous trouverez des informations sur mes compétences en tant que développeur web ainsi que mes projets récents. N'hésitez pas à me contacter si vous avez des questions ou des projets intéressants à partager.</p>
                <a class="projectsbutton" href="#projets">Découvrir mes projets</a>
            </div>
        </div>
    <section class="projects-section">
    <div class="alignfilter">
        <h1 class="projects-title" id="projets">MES PROJETS</h1>
        <br>
        <p style="text-align: center;">Filtre</p>
        <select name="filter" id="filter">
            <option value="Professionnel">Professionnel</option>
            <option value="Scolaire">Scolaire</option>
            <option value="Personnel">Personnel</option>
        </select>
    </div>
        <div v-html="projectsListHtml"></div>
        <div class="projectslist" v-if="filteredProjects">
            <nuxt-link :to="`/projects/${project.slug}`" v-for="project in filteredProjects.data">
                <div class="projects-container">
                    <img :src=project.image.url alt="" width="300">
                    <br>
                    <p>{{ project.name }}</p>
                </div>
            </nuxt-link>
        </div>
    </section>
    <section class="contact-section">
        <div class="spacing"></div>
        <div class="center-flex">
            <h1 class="type-color" id="contact">Contactez-moi</h1>
            <p class="text contact-text">Vous souhaitez en savoir plus ou discuter de vos projets ?<br>
            N'hésitez pas à me contacter !
            </p>
            <a class="contact-button" href="#">Me contacter</a>
        </div>
    </section>

    </div>
</template>

<script setup>

    const { find } = useStrapi()
    const projects = ref()
    const types = ref([])
    const activeFilter = ref('all')
    let filteredProjects = ref(projects);

    
    
    onMounted( async() =>{
        projects.value = await find('projets', {populate: 'deep'})
        types.value = new Set
        console.log(projects.value);
        let projectsData = projects.value.data;
        let filter = document.getElementById("filter");
        
       
        filter.addEventListener("change", function() {
            
            filteredProjects.value.data = [];
            
            for (let i = 0; i < projectsData.length; i++)
            {
                console.log(projectsData[i].project_type.type);
                if (projectsData[i].project_type.type == filter.value)
                {
                    filteredProjects.value.data.push(projectsData[i]);
                }
            }
            console.log(filteredProjects.value.data);
        })
        
    })
    
    
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400;500;600;700;800;900&family=Poiret+One&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Inter', sans-serif;
}

.alignfilter {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}


.contact-button {
    color: rgb(52, 99, 253);
    text-decoration: none;
    border: 1px solid rgb(52, 99, 253);
    width: 10%;
    text-align: center;
    padding: 15px 10px;
}


.center-flex {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 50px;
}

.contact-text {
    text-align: center;
}

.spacing {
    height: 10vh;
}

.contact-section {
    height: 60vh;
    background-color: rgb(44, 43, 43);
}

.projects-container p {
    text-align: center;
}

.projectslist {
    display: flex;
    gap: 5%;
    height: 50vh;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
}

.projects-title {
    color: rgb(52, 99, 253);
    margin: auto;
    text-align: center;
    margin-top: 50px;
    font-size: 35px;
}

.projects-section {
    height: 100vh;
}

.projectsbutton {
    color: rgb(52, 99, 253);
    text-decoration: none;
    border: 1px solid rgb(52, 99, 253);
    width: 40%;
    text-align: center;
    padding: 15px 10px;
    margin-top: 30px;
}

.text {
    color: rgb(89, 113, 133);
    font-weight: 300;
    letter-spacing: 1px;
}

.header-title {
    color: rgb(171, 216, 255);
    font-size: 40px;
}

.header-content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin: auto;
    width: 40%;
    height: 50%;
    margin-top: 50px;
}
.header-phrase {
    color: rgb(52, 99, 253);
    font-size: larger;
}

.header-container {
 height: 100vh;
 background-color: rgb(44, 43, 43);
}

.logo {
    color: white;
    font-size: 30;
    border: 1px solid rgb(52, 99, 253);
    padding: 10px 15px;

}

header {
    opacity: 0.80;
    height: 15vh;
    display: flex;
    align-items: center;
    justify-content: center;
}
.navwrapper {
    display: flex;
    justify-content: space-between;
    width: 90%;
    margin: auto;
}

.navlinks {
    display: flex;
    gap: 40px;
    list-style: none;
}

.navlinks li a {
    text-decoration: none;
    color: rgb(171, 216, 255);
    
}


</style>