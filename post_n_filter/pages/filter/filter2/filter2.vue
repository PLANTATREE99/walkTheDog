<template>
	<view class="page-content">
        <view @tap="orderbyChange" :class="{'text-theme': hasChoose}">
            <u-button>筛选按钮</u-button>
        </view>
        <fjj-condition ref='condition' @touchmove.stop :color="color" :list="menuList" :defaultValue="defaultValue" @result="resultConditon" />
    </view>
</template>

<script>
	import fjjCondition from '@/components/fjj-condition/fjj-condition.vue';
	    export default {
	        data() {
	            return {
	                hasChoose: false,
	                menuList: [],
	                defaultValue: {},
	            };
	        },
	        components: {
	            fjjCondition,
	        },
	        onLoad() {
	            setTimeout(() => {
	                this.menuList = [{
	                    'title': '多选',
	                    'type': 'custom',
	                    'key': 'custom1',
	                    'isMutiple': true, //多选
	                    'detailList': [{
	                        title: '多选选项1',
	                        value: "1",
	                        isSelected: true
	                    }, {
	                        title: '多选选项2',
	                        value: "2",
	                    }, {
	                        title: '多选选项3',
	                        value: "3",
	                    },
						],
	                }, {
	                    'title': '多选带更多',
	                    'type': 'custom',
	                    'key': 'custom3',
	                    'isMutiple': true, //多选
	                    'detailList': [{
	                        title: '多选选项1',
	                        value: "1",
	                    }, {
	                        title: '多选选项2',
	                        value: "2",
	                    }, {
	                        title: '多选选项3',
	                        value: "3",
	                    }, {
	                        title: '多选选项4',
	                        value: "4",
	                    }, {
	                        title: '多选选项5',
	                        value: "5",
	                    }, {
	                        title: '多选选项6',
	                        value: "6",
	                    }, {
	                        title: '多选选项7',
	                        value: "7",
	                    }],
	                }, {
	                    'title': '单选',
	                    'type': 'custom',
	                    'key': 'custom2',
	                    'isMutiple': false, //单选
	                    'detailList': [{
	                        title: '选项1',
	                        value: "1",
	                    }, {
	                        title: '选项2',
	                        value: "2",
	                    }],
	                }, {
	                    'title': '日期范围',
	                    'type': 'range',
	                    'key': 'time1',
	                    'minName': 'time1MinName',
	                    'maxName': 'time1MaxName',
	                }, {
	                    'title': '金额范围',
	                    'type': 'rangenumber',
	                    'key': 'count',
	                }, {
	                    'title': '输入框',
	                    'type': 'singleinput',
	                    'key': 'input',
	                }]
	                this.defaultValue = {
	                    custom1: ['1', '2'],
	                    custom3: ['2', '3'],
	                    custom2: 1,
	                    time1: ['2021/02/01', '2021/02/03'],
	                    time2: ['2021/10/01 00:00:00', '2021/10/07 23:59:59'],
	                    time3: '2021/04/01',
	                    count: [10, 20],
	                    input: 'fjj',
	                };
	            },2000)
	
	        },
	        methods: {
	            //筛选返回值
	            resultConditon(obj) {
	                this.$refs.condition.visibleDrawer = false;
	                this.hasChoose = obj.hasChoose;
	                console.log(obj);
	            },
	            orderbyChange(obj) {
	                this.$refs.condition.visibleDrawer = true;
	            }
	        }
	    

	}
</script>

<style>

</style>
