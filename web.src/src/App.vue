
<template>
  <a-layout>
    <a-layout-header style="padding: 10px;">
      <a-row>
        <a-col :span="3">
          <a-select size="large" type="primary" v-model="form.req.method">
            <a-option v-for="item in methods" :value="item.value" :label="item.label" />
          </a-select>
        </a-col>
        <a-col :span="18">
          <a-input size="large" v-model="form.req.url" placeholder="URL" />
        </a-col>
        <a-col :span="3">
          <a-button w size="large" type="primary" long @click="onSend">Send</a-button>
        </a-col>
      </a-row>
    </a-layout-header>
    <a-layout-content style="padding: 10px;">
      <a-collapse :default-active-key="['1']" :bordered="false">
        <a-collapse-item header="Request" key="1">
          <a-tabs type="capsule">
            <a-tab-pane key="1" title="Headers">
              Content of Tab Panel 1
            </a-tab-pane>
            <a-tab-pane key="2" title="Body">
              <a-textarea placeholder="Please enter something" allow-clear />
            </a-tab-pane>
          </a-tabs>

        </a-collapse-item>
        <a-collapse-item header="Response" key="3">
          <a-textarea v-model="form.resp.body" :auto-size="{minRows: 5 }" />
        </a-collapse-item>
      </a-collapse>
    </a-layout-content>
  </a-layout>

</template>


<script>
import aardio from 'aardio'

export default {
  data() {
    return {
      methods: [
        { label: "GET", value: "GET" },
        { label: "POST", value: "POST" },
        { label: "PUT", value: "PUT" },
        { label: "DELETE", value: "DELETE" },
        { label: "HEAD", value: "HEAD" },
        { label: "PATCH", value: "PATCH" },
        { label: "OPTIONS", value: "OPTIONS" }
      ],
      form: {
        req: {
          url: "https://mcd-api.tst.gululu.com/",
          method: "GET"
        },
        resp:{
          body: ""
        }
      }
    }
  },
  methods: {
    onSend(){
      aardio.httpRequest(this.form.req.url, "params", this.form.req.method, "headers")
      .then(resp=>{
        console.log("WEB >>", resp)
      })
      .catch (err => {
        console.log("err >>", err)
      })
    }
  },
  mounted() {
    console.log('xxxxxxxxxxxxx')
  }
}
</script>


<style>
@import './assets/base.css';

.arco-tabs-nav-tab {
  justify-content: flex-start !important;
}

.arco-collapse-item-content {
  background-color: var(--color-bg-1) !important;
}
</style>
