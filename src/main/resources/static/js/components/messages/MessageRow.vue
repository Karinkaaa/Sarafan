<template>
    <v-card class="my-2">
        <v-card-text primary-title>
            <div>
                <v-avatar
                        v-if="message.author && message.author.userpic"
                        size="56px"
                >
                    <img
                            :src="message.author.userpic"
                            :alt="message.author.name"
                    />
                </v-avatar>
                <v-avatar
                        v-else
                        color="indigo"
                        size="56px"
                >
                    <v-icon dark>account_circle</v-icon>
                </v-avatar>
                <span class="pl-3">{{ authorName }}</span>
            </div>
            <div class="pt-3"> {{ message.text }}</div>
        </v-card-text>
        <media v-if="message.link" :message="message"/>
        <v-card-actions>
            <v-btn value="Edit" @click="edit" small flat round>Edit</v-btn>
            <v-btn icon @click="del" small>
                <v-icon>delete</v-icon>
            </v-btn>
        </v-card-actions>
        <comment-list
                :comments="message.comments"
                :message-id="message.id"
        />
    </v-card>
</template>

<script>
    import {mapActions} from 'vuex'
    import Media from 'components/media/Media.vue'
    import CommentList from '../comment/CommentList.vue'

    export default {
        props: ['message', 'editMessage'],
        components: {CommentList, Media},
        computed: {
            authorName() {
                return this.message.author ? this.message.author.name : 'unknown';
            }
        },
        methods: {
            ...mapActions(['removeMessageAction']),
            edit() {
                this.editMessage(this.message);
            },
            del() {
                this.removeMessageAction(this.message);
            }
        }
    }
</script>

<style>
</style>