<template>
  <v-container>
    <v-card>
      <v-card-title primary-title>
        生成随机的 UUID
      </v-card-title>
      <v-card-text label="生成一个随机的 uuid">
        {{uuidStr}}
      </v-card-text>
      <v-card-actions>
        <v-btn
          color="success"
          @click="generator"
        >生成</v-btn>
      </v-card-actions>
    </v-card>
    <v-snackbar v-model="snackbarAction">
      {{snackbarText}}
      <v-btn
        flat
        color="primary"
        @click.native="snackbarAction = false"
      >Close</v-btn>
    </v-snackbar>
  </v-container>
</template>

<script>
import uuidv5 from 'uuid/v5'
import copy from 'copy-to-clipboard'

export default {
  data: () => ({
    uuidStr: '',
    snackbarAction: false,
    snackbarText: ''
  }),
  methods: {
    /**
     * 生成 uuid
     */
    generator () {
      this.uuidStr = uuidv5(Date.now().toString(), uuidv5.URL)
      this.copyToClipboard(this.uuidStr) ? this.success() : this.faild()
    },
    /**
     * 赋值内容到剪切板
     */
    copyToClipboard (str) {
      return copy(str)

    },
    success () {
      this.snackbarAction = true
      this.snackbarText = '复制成功，已经可以直接粘贴了'
    },
    faild () {
      this.snackbarAction = true
      this.snackbarText = '复制失败，请手动复制'
    }
  }
}
</script>