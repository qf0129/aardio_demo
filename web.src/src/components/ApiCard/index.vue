
<template>
    <a-card class="api_card" hoverable>
        <a-row>
            <a-col :span="3">
                <a-select size="large" type="primary" v-model="form.req.method">
                    <a-option v-for="item in methods" :value="item.value" :label="item.label" />
                </a-select>
            </a-col>
            <a-col :span="20">
                <a-input size="large" v-model="form.req.url" placeholder="URL" />
            </a-col>
            <a-col :span="1">
                <a-button type="text" shape="circle" style="float: right; font-size: 20px; color: #aaa;">
                    <icon-close />
                </a-button>
            </a-col>
        </a-row>
        <a-card :bordered="false">
            <a-tabs type="capsule">
                <a-tab-pane key="1" title="Headers">
                    <a-textarea placeholder="Please enter something" allow-clear />
                </a-tab-pane>
                <a-tab-pane key="2" title="Body">
                    <a-textarea placeholder="Please enter something" allow-clear />
                </a-tab-pane>
            </a-tabs>
        </a-card>
        <a-row>
            <a-col>
                <a-button w size="large" type="primary" long @click="onSend">Send</a-button>
            </a-col>
        </a-row>
        <a-grid :cols="3" :colGap="12" :rowGap="16" class="grid-demo-grid" :collapsed="false">
            <a-grid-item class="demo-item">item</a-grid-item>
            <a-grid-item class="demo-item">item</a-grid-item>
            <a-grid-item class="demo-item">item</a-grid-item>
            <a-grid-item class="demo-item" :offset="1">item | offset - 1</a-grid-item>
            <a-grid-item class="demo-item">item</a-grid-item>
            <a-grid-item class="demo-item" :span="3">item | span - 3</a-grid-item>
            <a-grid-item class="demo-item">item</a-grid-item>
            <a-grid-item class="demo-item">item</a-grid-item>
            <a-grid-item class="demo-item" suffix #="{ overflow }">
                suffix | overflow: {{ overflow }}
            </a-grid-item>
        </a-grid>
    </a-card>
</template>


<script>
import aardio from 'aardio'
import { IconClose } from '@arco-design/web-vue/es/icon';


export default {
    components: {
        IconClose
    },
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
                resp: {
                    body: ""
                }
            }
        }
    },
    methods: {
        onSend() {
            aardio.httpRequest(this.form.req.url, "params", this.form.req.method, "headers")
                .then(resp => {
                    console.log("WEB >>", resp)
                })
                .catch(err => {
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
.arco-tabs-nav-tab {
    justify-content: flex-start !important;
}

.arco-collapse-item-content {
    background-color: var(--color-bg-1) !important;
}

.api_card {
    /* border: 1px solid #333; */
    /* margin: 10px auto;
    padding: 10px;
    width: 90%; */
    margin-bottom: 20px;
}
</style>
