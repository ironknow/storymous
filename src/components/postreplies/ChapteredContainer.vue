<template>
    <div>
        <div :class="outlineClass">
            <span @click="navigateToPost" style="text-decoration: none;" >
                <div class="story__user-container">
                    <div class="story__user-img-container">
                        <span @click.stop="navigateToUser" style="color: inherit; text-decoration: none;">
                            <img :src="imgSource" v-if="picture" alt="pic" class="story__user-img">
                        </span>
                    </div> 
                    <div class="story__user-info-container">
                        <div class="story__username cur-pnt"> 
                            <span @click.stop="navigateToUser" style="color: inherit; text-decoration: none;">
                                <span class="lower" style="color: whitesmoke;"><b>@</b></span><b class="story__user-name">{{ username }}</b>
                            </span>
                                <span class="story__username-date lower cur-def">· {{ date }} </span>
                        </div>
                    </div>
                </div>
                <article class="story__article">
                    <div class="story__upper">
                        <h2 class="story__title "><span class="story_title highlight1">CHAPTER</span><span class="story_title highlight">{{ chapterNum }}</span>{{ chapterName.toUpperCase() }}</h2>
                    </div>      
                    <p class="story__content">
                        {{ formatStory(content) }}
                    </p>
                </article>
            </span>
        </div>
    </div>
</template>

<script>
import { useRouter } from 'vue-router';

export default {

    setup() {
        const router = useRouter();
        return { router: router };
    },
    props: ["_id", "content", "username", "postComment", "color", "date", "picture", "chapterNum", "storyId", "parentChapterId", "chapterName", "tags", "feedMode"],
    methods: {
        formatStory(story) {
            const formattedStory = story.replace(/<br>/g, '\n')
            if (formattedStory.length > 700 && this.feedMode) {
                return formattedStory.substring(0, 700) + '...';
            }
            return formattedStory
        },
        navigateToPost() {
            this.router.push('/chapter/' + this._id.$oid);
        },
        navigateToUser() {
            this.router.push('/user/' + this.username);
        }
    },

    computed: {
        imgSource() {
            return require('@/assets/img/' + this.picture);
        },
        outlineClass() {
            return `outline ${this.color}`;
        },
        checkLength() {
            if (this.content.length >= 697) {
                return true
            }
            return false
        }
    },
    
};
</script>

<style scoped>
.highlight {
    background-color: bisque;
    color: black;
    border-radius: 2px;
    padding: 0 3px;
    margin: 0 8px 0 0px;
    font-size: 17px;
}

.highlight1 {
    background-color: bisque;
    color: black;
    border-radius: 2px;
    padding: 0 3px;
    margin: 0 4px 0 0px;
    font-size: 17px;
}

.story__upper {
    display: flex;
    margin: 5px 0 5px 0;
    font-weight: bold;
}   

.story__title {
    color: bisque;
    font-size: 17px;
    align-self: center;
    justify-self: center;
    margin: 0px 0px 0px 0px;
    font-weight: bold;
}

.origin {
    background-color: rgba(160, 160, 160, 0.247);
    color: rgb(255, 255, 255);
    font-size: 14px;
    padding: 0px 3px;
    border-radius: 1px;
    width: fit-content;
    box-shadow: 0px 0px 2px rgba(128, 128, 128, 0.568);
    
}

.origin-container {
    display: flex;
    justify-content: flex-start;
    margin: 2px 5px 0 5px;
}


.story__article {
    border-radius: 0px;
    cursor: pointer;
    transition: all 0s;
    color: #d3d3d3;

}


.story__user-container {
    padding: 5px 0 0 0px;
    display: flex;
    flex-direction: row;
    border-top: 1px rgba(129, 129, 129, 0.322) solid;
}

.story__user-img-container {
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
}

.story__user-comment-container {
    max-width: fit-content;
    word-wrap: break-word;
}

.story__user-comment {
    margin-top: 0px;
    font-weight: bold;
    color: black;
    background-color: #faf8f8;
    padding: 5px 10px;
    border-radius: 15px 15px 15px 0;
    text-align: left;
    word-wrap: break-word;
    hyphens: auto;
    width: auto;
}

.story__user-info-container {
    display: flex;
    flex-direction: column;
    margin: 0 0 0 5px;
    width: fit-content;
    hyphens: auto;
    justify-content: space-between;
}

.story__title-container {
    background-color: rgb(255, 214, 164);
    padding: 2px;
    justify-content: left;
    border-radius: 5px;
    margin-bottom: 8px;
    width: 100%;
    word-wrap: break-word;
    hyphens: auto;
}


.story__content {
    text-align: left;
    margin: 2px 0;
    white-space: pre-wrap;
}

.readmore-button {
    white-space: nowrap;
    font-weight: bolder;
    color: #dddddd;
}

.readmore-button:hover {
    text-decoration: underline 2px;
}

.story__username-date {
    margin: 0 0 0 5px;
    font-size: 12px;
    color: whitesmoke;
    font-weight: normal;
}

.story__user-name {
    color: whitesmoke;
    text-decoration: none;
    margin: 0 4px 0 0;
}

.story__user-name:hover {
    text-decoration: underline 2px;
}

.story__username {
    margin: 0px 0px;
    font-size: 14px;
}

.story__user-img {
    width: 25px;
    height: auto;
    border-radius: 100%;
    cursor: pointer;
    transition: all 0.1s;
    margin-top: 2px;
}

.story__user-img:hover {
    filter: brightness(85%);
}

.story__user-img-container {
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
}

.post__story {
    box-shadow: 0 0 10px 0 #3c4755;
    margin-bottom: 10px;
}

.story__user-info-container {
    display: flex;
    flex-direction: column;
    margin: 0 0 0 5px;
    width: fit-content;
    hyphens: auto;
    justify-content: center;
    align-items: center;
}

.story__user-comment {
    margin-top: 0px;
    font-weight: bold;
    color: black;
    background-color: #faf8f8;
    padding: 5px 10px;
    border-radius: 15px 15px 15px 0;
    text-align: left;
    word-wrap: break-word;
    hyphens: auto;
    width: auto;
}

.story__username {
    margin: 5px 0px;
}

.story__user-tags {
    margin-top: 8px;
    display: flex;
    flex-direction: row;
}

.story__tag {
    border-radius: 15px;
    padding: 1px 8px;
    color: white;
    opacity: 0.8;
    margin-right: 5px;
}

.post-icons-bar {
    display: flex;
    justify-content: right;
    font-size: 13px;
    height: fit-content
}

.post-icon-bg {
    height: fit-content;
    padding: 0 4px;
    display: flex;
    background-color: rgba(240, 248, 255, 0);
    border-radius: 10px;
    opacity: 1;
}

.post-icon-bg:hover {
    cursor: pointer;
    display: flex;
    background-color: rgba(240, 248, 255, 0.219);
    border-radius: 12px;
}


.post-icons {
    background-color: #31394600;
    margin: 5px 0 0px 0;
    padding: 2px 4px 0px 5px;
    /*border-radius: 5px;*/
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    width: fit-content;
    height: fit-content;
    align-items: center;
}

</style>