<template>
	<view class="content">

		<u-divider text="图片上传"></u-divider>
		<u-upload :fileList="fileList1" @afterRead="afterRead" @delete="deletePic"
				name="1" multiple:maxCount="5" :previewFullImage="true"></u-upload>		
		<u-divider text="详细信息"></u-divider>
		<!--选择-->
		<view id="selector">
			<u-radio-group v-model="radiovalue1" placement="row" @change="groupChange">
				<u-radio v-for="(item, index) in radiolist1" 
				:key="index" :label="item.name" :name="item.name" @change="radioChange"></u-radio>
			</u-radio-group>
			<view id="switch">
				<p>已注射疫苗</p>
				<u-switch v-model="value1" @change="change"></u-switch>
			</view>
			<!--下拉选择-->
			<u-picker :show="show" :columns="columns">
				<u-toolbar @cancel="show=false"> 
				</u-toolbar>
			</u-picker>
			<u-button id="pickerBtn" type="info" @click="show=true" shape="circle">年龄</u-button>
			
		</view>
		<!--自由输入-->
		<u--textarea v-model="value2" placeholder="再多点介绍" ></u--textarea>
	
		<view id="btnContainer">
			<u-button >保存</u-button>
			<u-button :customStyle="float='right'">发布</u-button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				fileList1: [],
				
				value1: true,
				
				show: false,
                columns: [
                    ['1', '2', '3']
                ],
				
				radiolist1: [{
				            name: 'M',
				            disabled: false
						},
				            {
				            name: 'F',
				            disabled: false,
							},
				],
				radiovalue1:'F',
				
				value2: '',
				
			}
			
		},
		methods: {
			//上传照片
			// 删除图片
			deletePic(event) {
				this[`fileList${event.name}`].splice(event.index, 1)
			},
			// 新增图片
			async afterRead(event) {
				// 当设置 mutiple 为 true 时, file 为数组格式，否则为对象格式
				let lists = [].concat(event.file)
				let fileListLen = this[`fileList${event.name}`].length
				lists.map((item) => {
					this[`fileList${event.name}`].push({
						...item,
						status: 'uploading',
						message: '上传中'
					})
				})
				for (let i = 0; i < lists.length; i++) {
					const result = await this.uploadFilePromise(lists[i].url)
					let item = this[`fileList${event.name}`][fileListLen]
					this[`fileList${event.name}`].splice(fileListLen, 1, Object.assign(item, {
						status: 'success',
						message: '',
						url: result
					}))
					fileListLen++
				}
			},
			uploadFilePromise(url) {
				return new Promise((resolve, reject) => {
					let a = uni.uploadFile({
						url: 'http://192.168.2.21:7001/upload', // 仅为示例，非真实的接口地址
						filePath: url,
						name: 'file',
						formData: {
							user: 'test'
						},
						success: (res) => {
							setTimeout(() => {
								resolve(res.data.data)
							}, 1000)
						}
					});
				})
			},
			change(e) {
				console.log('change', e);
			},
		}

	}
</script>

<style>
	#pickerBtn {
		margin-top: 1rem;
		margin-left: 0;
		border: solid;
		border-color: royalblue;
		width: 5rem;
		
	}
	#btnContainer{
		display: flex;
		float: right;
		margin-top: 2rem;
	}
	#selector{
		display: block;
		margin: 5% auto;
	}
	#switch{
		display: flex;
		margin: 5% auto;
		float: right;
	}
</style>
