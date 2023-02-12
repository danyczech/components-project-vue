<template>
    <BaseCard>
        <BaseButton @click="setSelectedTab('StoredResources')" :mode="storedResButtonMode">Stored Resources</BaseButton>
        <BaseButton @click="setSelectedTab('AddResource')" :mode="addResButtonMode">Add Resource</BaseButton>
    </BaseCard>
    <keep-alive>
        <component :is="selectedTab">
        </component>
    </keep-alive>


</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
    components: {
        StoredResources,
        AddResource
    },
    data() {
        return {
            selectedTab: 'StoredResources',
            storedResources: [
                {id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official Vue.js documentation',
                    link: 'https://vuejs.org'
                },
                {id: 'google',
                    title: 'Google',
                    description: 'Learn to google...',
                    link: 'https://google.org'
                },
            ]
        }
    },
    provide() {
        return {
            resources: this.storedResources,
            addResource: this.addResource
        };
    },
    computed: {
        storedResButtonMode() {
            return this.selectedTab === 'StoredResources' ? null : 'flat';
        },
        addResButtonMode(){
            return this.selectedTab === "AddResource" ? null : 'flat';
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addResource(title, description, link) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: link
            }
            this.storedResources.unshift(newResource);
            this.selectedTab = 'StoredResources';
        }
    }
}
</script>