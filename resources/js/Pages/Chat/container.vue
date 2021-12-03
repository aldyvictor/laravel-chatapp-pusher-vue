<template>
    <app-layout title="Chat">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Chat
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <message-container />
                    <input-message :room="currentRoom" />
                </div>
            </div>
        </div>
    </app-layout>
</template>

<script>
import { defineComponent } from "vue";
import AppLayout from "@/Layouts/AppLayout.vue";
import MessageContainer from "./messageContainer.vue";
import InputMessage from "./inputMessage.vue";

export default defineComponent({
    components: {
        AppLayout,
        MessageContainer,
        InputMessage,
    },
    data: function () {
        return {
            chatRoom: [],
            currentRoom: [],
            messages: [],
        };
    },
    methods: {
        getRoom() {
            axios
                .get("/chat/rooms")
                .then((response) => {
                    this.chatRoom = response.data;
                    this.setRoom(response.data[0]);
                })
                .catch((error) => {
                    console.log(error);
                });
        },
        setRoom(room) {
            this.currentRoom = room;
            this.getMessages();
        },
        getMessages() {
            axios
                .get("/chat/room/" + this.currentRoom.id + "/messages")
                .then((response) => {
                    this.messages = response.data;
                })
                .catch((error) => {
                    console.log(error);
                });
        },
    },
    created() {
        this.getRoom();
    },
});
</script>
