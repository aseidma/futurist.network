<template>
  <div class="container">
    <div
      class="mt-5 d-flex flex-column justify-content-center align-items-center"
    >
      <CenteredHero
        icon="../../icons/projects.svg"
        title="Projects"
        desc="Discover student and community made projects!"
        arrowLink="#projects"
      />
    </div>
    <a id="projects" />
    <div class="project-cards-container">
      <ProjectCard
        v-for="(project, index) in projects"
        :key="index"
        :project="project"
      />
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({$content, params, error}) {
    const projectsDataStore = await $content('projects').fetch()
    const projects = []
    for (const projectData of projectsDataStore[0].projects) {
      const project = {
        title: projectData.name,
        desc: projectData.desc,
        repo: projectData.repo,
        logo: projectData.logo,
        link: projectData.link,
        tags: projectData.tags,
        status: projectData.status,
        discord: projectData.discord,
      }
      projects.push(project)
    }
    return {projects}
  },
}
</script>

<style scoped>
.project-cards-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.resource-tag {
  text-transform: capitalize;
}
</style>
