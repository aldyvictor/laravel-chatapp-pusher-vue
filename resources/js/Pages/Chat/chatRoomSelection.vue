<template>
    <div class="grid grid-cols-2">
        <div class="font-bold text-xl">{{ selected.name }} Chat</div>
        <div>
            <select v-model="selected" @change="push" class="float-right">
                <option
                    :value="room"
                    v-for="(room, index) in rooms"
                    :key="index"
                >
                    {{ room.name }}
                </option>
            </select>
        </div>
    </div>
</template>

<script>
export default {
    props: ["rooms", "currentRoom"],
    data: function () {
        return {
            selected: "",
        };
    },
    methods: {
        push() {
            this.$emit("roomchanged", this.selected);
        },
    },
    created() {
        this.selected = this.currentRoom;
    },
};
</script>
