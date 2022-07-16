
<template>
    <div class="api_card" hoverable>
        <a-row style="padding:10px;">
            <a-col :span="3">
                <a-select size="large" type="primary" v-model="form.req.method">
                    <a-option v-for="item in methods" :value="item.value" :label="item.label" />
                </a-select>
            </a-col>
            <a-col :span="17">
                <a-input size="large" v-model="form.req.url" placeholder="URL" />
            </a-col>
            <a-col :span="3">
                <a-button w size="large" type="primary" long @click="onSend">Send</a-button>
            </a-col>
            <a-col :span="1">
                <a-button type="text" shape="circle" style="float: right; font-size: 16px; color: #aaa;">
                    <icon-close />
                </a-button>
            </a-col>
        </a-row>
        <div v-if="showMore" style="padding: 10px;">
            <a-tabs type="capsule">
                <a-tab-pane key="1" title="Headers">
                    <a-textarea placeholder="Please enter something" allow-clear />
                </a-tab-pane>
                <a-tab-pane key="2" title="Body">
                    <a-textarea placeholder="Please enter something" allow-clear />
                </a-tab-pane>
            </a-tabs>
        </div>
        <!-- <a-row style="padding:10px;" v-if="showMore">
            <a-col :span="20" ></a-col>
            <a-col :span="4">
                <a-button w size="large" type="primary" long @click="onSend">Send</a-button>
            </a-col>
        </a-row> -->
        <div class="showMoreBar" style="text-align: center;" @click="showMore=!showMore">
            <icon-double-up v-if="showMore" />
            <icon-double-down v-else />
        </div>
    </div>
</template>


<script>
import aardio from 'aardio'
import { IconClose, IconDoubleDown, IconDoubleUp } from '@arco-design/web-vue/es/icon';


export default {
    components: {
        IconClose, IconDoubleDown, IconDoubleUp
    },
    data() {
        return {
            showMore: false,
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


<style lang="scss">
.arco-tabs-nav-tab {
    justify-content: flex-start !important;
}

.arco-collapse-item-content {
    background-color: var(--color-bg-1) !important;
}

.api_card {
    border: 1px solid #dadada;
    /* margin: 10px auto;
    padding: 10px;
    width: 90%; */
    margin-bottom: 10px;
}
.demo-item{
    border: 1px solid #333;
}
.showMoreBar{
    color: #aaa;
    cursor: pointer;
    text-align: center;
    &:hover{
        color: #165dff;
        background-image: linear-gradient(#fff, #eee);
    }
}
</style>
