<template>
    <div class="component_panel">

        <ul>
            <li @click="tabChange(index)" :class="tabSelected == index ? 'active' : ''" :key="item.id"
                v-for="(item, index) in templateNode">
                {{ item.tag }}</li>
        </ul>
        <div class="component_options" :class="tabSelected == index ? 'current' : ''" v-for="(item, index) in templateNode">
            <ul>
                <li v-for="t in item.componentData" :key="t.cid" @click="addComponent(t.template)">
                    <img :src="t.imgSrc" />
                    <span>{{ t.cname }}</span>
                </li>
            </ul>
        </div>
    </div>
</template>
<script setup>
import { ref } from 'vue';
import { mainStore } from '../../store/index'
const tabSelected = ref(0)
const store = mainStore()
const tabChange = (index) => {
    tabSelected.value = index
}
const addComponent = (node) => {
    // console.log(node);
    store.addComponent(node)
}
const templateNode = [
    {
        id: 1,
        tag: '容器',
        componentData: [{
            cid: 1,
            cname: '按钮',
            imgSrc: '/src/assets/vue.svg',
            template:
            {
                tag: 'Button',
                props: {},
                values: {
                    text: '测试按钮'
                },
                childrens: []
            }
        }]
    },
    {
        id: 2,
        tag: '组件',
        componentData: [{
            cid: 1,
            cname: '纵向布局',
            imgSrc: '/src/assets/vue.svg',
            template: {
                tag: 'LayoutContent',
                props: {
                    style: {}
                },
                values: {},
                childrens: []
            }

        }]

    }
]
</script>
<style  scoped>
.component_panel {
    width: 250px;
    height: 100%;
    margin: 0 auto;
}

ul {
    display: flex;
    list-style: none;

}

.component_panel>ul li {
    width: 120px;
    height: 36px;
    text-align: center;
    line-height: 36px;
    color: #333333;
    font-weight: bold;
    border: 1px solid #bfbfbf;
    transition: ease-in-out all 0.3s;
    cursor: pointer;
}

.component_panel>ul li:hover {
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.25);
}

.current {
    display: block !important;
}

.active {
    color: #ffffff !important;
    background: #4a8af4;
}

/* 下方的内容 */
.component_options {
    display: none;
}

.component_options ul>li {
    cursor: pointer;
}

.component_options ul>li>img {
    margin: 17px 24px 8px;
    width: 32px;
}

.component_options ul>li>span {
    display: block;
    text-align: center;
    font-size: 14px;
    color: #666666;
}
</style>