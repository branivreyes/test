<script setup lang="ts">
import { ref } from "vue";
import Message from "@/components/Message.vue";
import { onMounted } from "vue";
import { nextTick } from "vue";
import type { VForm } from "vuetify/lib/components/index";
import { chatInputRules } from "@/types/rules";

const chats = ref([
  {
    type: "subheader",
    title: "Today",
  },
  {
    prependAvatar: "https://cdn.vuetifyjs.com/images/lists/1.jpg",
    title: "Ali Connors",
    subtitle: "Lorem ipsum...",
  },
  {
    type: "divider",
    inset: true,
  },
  {
    prependAvatar: "https://cdn.vuetifyjs.com/images/lists/2.jpg",
    title: "Alex",
    subtitle: "Lorem ipsum...",
  },
  {
    type: "divider",
    inset: true,
  },
  {
    prependAvatar: "https://cdn.vuetifyjs.com/images/lists/3.jpg",
    title: "Jennifer",
    subtitle: "Lorem ipsum...",
  },
  {
    type: "divider",
    inset: true,
  },
  {
    prependAvatar: "https://cdn.vuetifyjs.com/images/lists/4.jpg",
    title: "Sandra Adams",
    subtitle: "Lorem ipsum...",
  },
]);

const messages = ref([
  {
    message: "Lorem ipsum...",
    byOwner: true,
  },
  {
    message: "Lorem ipsum...",
    byOwner: false,
  },
  {
    message: "Lorem ipsum...",
    byOwner: true,
  },
  {
    message: "Lorem ipsum...",
    byOwner: true,
  },
  {
    message: "Lorem ipsum...",
    byOwner: false,
  },
  {
    message: "Lorem ipsum...",
    byOwner: false,
  },
  {
    message: "Lorem ipsum...",
    byOwner: false,
  },
  {
    message: "Lorem ipsum...",
    byOwner: false,
  },
  {
    message: "Lorem ipsum...",
    byOwner: false,
  },
  {
    message: "Lorem ipsum...",
    byOwner: false,
  },
]);

const messagesScroll = ref<HTMLDivElement | null>(null);

const message = ref("");

const chatForm = ref<VForm | null>(null);

function scrollToBottom() {
  messagesScroll.value?.scrollTo(0, messagesScroll.value.scrollHeight);
}

async function sendMessage() {
  const validated = await chatForm.value?.validate();

  if (!validated?.valid) return;

  messages.value.push({
    message: message.value,
    byOwner: true,
  });

  message.value = "";

  nextTick(() => {
    scrollToBottom();
  });
}

onMounted(() => {
  scrollToBottom();
});
</script>

<template>
  <v-container
    class="bg-grey-lighten-1 mx-0"
    style="width: 100% !important; max-width: 100%; height: 100%"
  >
    <v-row style="height: 100%">
      <v-col cols="2">
        <v-sheet rounded="lg">
          <v-list rounded="lg" :items="chats" item-props lines="two">
            <template v-slot:subtitle="{ subtitle }">
              <div>{{ subtitle }}</div>
            </template>
          </v-list>
        </v-sheet>
      </v-col>
      <v-col>
        <v-sheet rounded="lg" class="chat-container">
          <div class="bg-grey-lighten-2 messages-container">
            <v-list lines="one">
              <v-list-item title="Lorem ipsum" subtitle="Online"> </v-list-item>
            </v-list>
            <div class="messages pa-2">
              <div class="container" ref="messagesScroll">
                <message
                  v-for="(message, index) in messages"
                  :key="index"
                  :message="message.message"
                  :by-owner="message.byOwner"
                />
              </div>
            </div>
          </div>
          <v-form
            class="bg-grey-lighten pa-2 chat-input"
            @submit.prevent="sendMessage"
            ref="chatForm"
          >
            <v-btn icon="mdi-paperclip"></v-btn>
            <v-text-field
              v-model="message"
              class="mx-2"
              variant="solo"
              hide-details
              placeholder="Type a message"
              :rules="chatInputRules"
            ></v-text-field>
            <v-btn
              :disabled="!message"
              type="submit"
              color="primary"
              icon="mdi-send"
            ></v-btn>
          </v-form>
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped lang="scss">
.chat-container {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  overflow: hidden;

  .messages-container {
    flex-grow: 1;
    display: flex;
    flex-direction: column;

    .messages {
      flex-grow: 1;
      position: relative;
      .container {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        overflow-y: auto;
      }

      &:deep(.message-container) {
        margin-bottom: 20px;
      }
    }
  }

  .chat-input {
    display: flex;
    align-items: center;
  }
}
</style>
