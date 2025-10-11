<template>
	<div class="main-content" :style='{"minHeight":"100vh","padding":"78px 10px","fontSize":"15px","background":"#E2E2E2"}'>
		<!-- 列表页 -->
		<template v-if="showFlag">
			<el-form class="center-form-pv" :style='{"margin":"0 0px 20px 0","background":"none"}' :inline="true" :model="searchForm">
				<el-row :style='{"padding":"10px 0","alignItems":"center","flexWrap":"wrap","background":"none","display":"flex"}' >
					<div :style='{"alignItems":"center","margin":"0 10px 10px 0","display":"flex"}'>
						<label :style='{"margin":"0 10px 0 0","whiteSpace":"nowrap","color":"#000000","textAlign":"right","width":"auto","lineHeight":"40px","fontSize":"14px","fontWeight":"400","height":"40px"}' class="item-label">中文名</label>
						<el-input v-model="searchForm.cname" placeholder="中文名" @keydown.enter.native="search()" clearable></el-input>
					</div>
					<div :style='{"alignItems":"center","margin":"0 10px 10px 0","display":"flex"}'>
						<label :style='{"margin":"0 10px 0 0","whiteSpace":"nowrap","color":"#000000","textAlign":"right","width":"auto","lineHeight":"40px","fontSize":"14px","fontWeight":"400","height":"40px"}' class="item-label">食品分类</label>
						<el-input v-model="searchForm.spfenlei" placeholder="食品分类" @keydown.enter.native="search()" clearable></el-input>
					</div>
					<div :style='{"alignItems":"center","margin":"0 10px 10px 0","display":"flex"}'>
						<label :style='{"margin":"0 10px 0 0","whiteSpace":"nowrap","color":"#000000","textAlign":"right","width":"auto","lineHeight":"40px","fontSize":"14px","fontWeight":"400","height":"40px"}' class="item-label">产地</label>
						<el-input v-model="searchForm.chandi" placeholder="产地" @keydown.enter.native="search()" clearable></el-input>
					</div>
					<el-button class="search" type="success" @click="search()">
						<span class="icon iconfont icon-fangdajing07" :style='{"margin":"0 2px","fontSize":"16px","color":"#fff","height":"40px"}'></span>
						查询
					</el-button>
				</el-row>

				<el-row class="actions" :style='{"padding":"10px 0","margin":"0px 0","flexWrap":"wrap","background":"none","display":"flex"}'>
					<el-button class="add" v-if="isAuth('eshianyycf','新增')" type="success" @click="addOrUpdateHandler()">
						<span class="icon iconfont icon-tianjia14" :style='{"margin":"0 2px","fontSize":"14px","color":"#fff","height":"34px"}'></span>
						新增
					</el-button>
					<el-button class="del" v-if="isAuth('eshianyycf','删除')" :disabled="dataListSelections.length?false:true" type="danger" @click="deleteHandler()">
						<span class="icon iconfont icon-shanchu6" :style='{"margin":"0 2px","fontSize":"14px","color":"#fff","height":"34px"}'></span>
						删除
					</el-button>


					<el-button class="btn18" v-if="isAuth('eshianyycf','爬取数据')" type="success" @click="spider()">
						<span class="icon iconfont icon-shuju20" :style='{"margin":"0 2px","fontSize":"14px","color":"#fff","height":"34px"}'></span>
						爬取数据
					</el-button>
					<el-button class="btn18" v-if="isAuth('eshianyycf','食物词云')" type="success" @click="chartDialog1()">
						<span class="icon iconfont icon-zhangjie2" :style='{"margin":"0 2px","fontSize":"14px","color":"#fff","height":"34px"}'></span>
						食物词云
					</el-button>
					<el-button class="btn18" v-if="isAuth('eshianyycf','食物类型分布')" type="success" @click="chartDialog2()">
						<span class="icon iconfont icon-zhangjie2" :style='{"margin":"0 2px","fontSize":"14px","color":"#fff","height":"34px"}'></span>
						食物类型分布
					</el-button>
					<el-button class="btn18" v-if="isAuth('eshianyycf','产地分布')" type="success" @click="chartDialog3()">
						<span class="icon iconfont icon-zhangjie2" :style='{"margin":"0 2px","fontSize":"14px","color":"#fff","height":"34px"}'></span>
						产地分布
					</el-button>
					<el-button class="btn18" v-if="isAuth('eshianyycf','能量区间')" type="success" @click="chartDialog4()">
						<span class="icon iconfont icon-zhangjie2" :style='{"margin":"0 2px","fontSize":"14px","color":"#fff","height":"34px"}'></span>
						能量区间
					</el-button>
					<el-button class="btn18" v-if="isAuth('eshianyycf','蛋白质排名')" type="success" @click="chartDialog5()">
						<span class="icon iconfont icon-zhangjie2" :style='{"margin":"0 2px","fontSize":"14px","color":"#fff","height":"34px"}'></span>
						蛋白质排名
					</el-button>
					<el-button class="btn18" v-if="isAuth('eshianyycf','碳水化合物排名')" type="success" @click="chartDialog6()">
						<span class="icon iconfont icon-zhangjie2" :style='{"margin":"0 2px","fontSize":"14px","color":"#fff","height":"34px"}'></span>
						碳水化合物排名
					</el-button>
				</el-row>
			</el-form>
			<div :style='{"width":"100%","padding":"0 10px","fontSize":"14px","color":"#000"}'>
				<el-table class="tables"
					:stripe='true'
					:style='{"padding":"10px 0","borderColor":"#eee","borderRadius":"20px 20px 0 0","borderWidth":"1px 0 0 1px","background":"#fff","width":"100%","fontSize":"inherit","borderStyle":"solid"}' 
					:border='true'
					v-if="isAuth('eshianyycf','查看')"
					:data="dataList"
					v-loading="dataListLoading"
				@selection-change="selectionChangeHandler">
					<el-table-column :resizable='true' type="selection" align="center" width="50"></el-table-column>
					<el-table-column :resizable='true' :sortable='true' label="序号" type="index" width="50" />
					<el-table-column :resizable='true' :sortable='true'  
						prop="cname"
						label="中文名">
						<template slot-scope="scope">
							{{scope.row.cname}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="ename"
						label="英文名">
						<template slot-scope="scope">
							{{scope.row.ename}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="spfenlei"
						label="食品分类">
						<template slot-scope="scope">
							{{scope.row.spfenlei}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="keshibu"
						label="可食部%">
						<template slot-scope="scope">
							{{scope.row.keshibu}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="laiyuan"
						label="来源">
						<template slot-scope="scope">
							{{scope.row.laiyuan}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="chandi"
						label="产地">
						<template slot-scope="scope">
							{{scope.row.chandi}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="nengliang"
						label="能量(千焦)">
						<template slot-scope="scope">
							{{scope.row.nengliang}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="danbaizhi"
						label="蛋白质(克)">
						<template slot-scope="scope">
							{{scope.row.danbaizhi}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="zhifang"
						label="脂肪(克)">
						<template slot-scope="scope">
							{{scope.row.zhifang}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="tshhw"
						label="碳水化合物(克)">
						<template slot-scope="scope">
							{{scope.row.tshhw}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="dangc"
						label="胆固醇(毫克)">
						<template slot-scope="scope">
							{{scope.row.dangc}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="baohezhifang"
						label="饱和脂肪酸(克)">
						<template slot-scope="scope">
							{{scope.row.baohezhifang}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="fanshizfs"
						label="反式脂肪酸(克)">
						<template slot-scope="scope">
							{{scope.row.fanshizfs}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="dbbhzfs"
						label="单不饱和脂肪酸(克)">
						<template slot-scope="scope">
							{{scope.row.dbbhzfs}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="duobbhzfs"
						label="多不饱和脂肪酸(克)">
						<template slot-scope="scope">
							{{scope.row.duobbhzfs}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="tang"
						label="糖(克)">
						<template slot-scope="scope">
							{{scope.row.tang}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="rutang"
						label="乳糖(克)">
						<template slot-scope="scope">
							{{scope.row.rutang}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="sanshiqw"
						label="膳食纤维(克)">
						<template slot-scope="scope">
							{{scope.row.sanshiqw}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="kesxssqw"
						label="可溶性膳食纤维(克)">
						<template slot-scope="scope">
							{{scope.row.kesxssqw}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="bsxssqw"
						label="不溶性膳食纤维(克)">
						<template slot-scope="scope">
							{{scope.row.bsxssqw}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="jinshuna"
						label="钠(毫克)">
						<template slot-scope="scope">
							{{scope.row.jinshuna}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="weishengshua"
						label="维生素A(微克视黄醇当量)">
						<template slot-scope="scope">
							{{scope.row.weishengshua}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="weishengshud"
						label="维生素D(微克)">
						<template slot-scope="scope">
							{{scope.row.weishengshud}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="weishengshue"
						label="维生素E(毫克α-生育酚当量)">
						<template slot-scope="scope">
							{{scope.row.weishengshue}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="weishengshuk"
						label="维生素K(微克)">
						<template slot-scope="scope">
							{{scope.row.weishengshuk}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="weishengshub1"
						label="维生素B1（硫胺素）(毫克)">
						<template slot-scope="scope">
							{{scope.row.weishengshub1}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="weishengshub2"
						label="维生素B2（核黄素）(毫克)">
						<template slot-scope="scope">
							{{scope.row.weishengshub2}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="weishengshub6"
						label="维生素B6(毫克)">
						<template slot-scope="scope">
							{{scope.row.weishengshub6}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="weishengshub12"
						label="维生素B12(微克)">
						<template slot-scope="scope">
							{{scope.row.weishengshub12}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="weishengshuc"
						label="维生素C（抗坏血酸）(毫克)">
						<template slot-scope="scope">
							{{scope.row.weishengshuc}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="yanshuan"
						label="烟酸（烟酰胺）(毫克)">
						<template slot-scope="scope">
							{{scope.row.yanshuan}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="yeshuan"
						label="叶酸(微克叶酸当量)">
						<template slot-scope="scope">
							{{scope.row.yeshuan}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="fanshuan"
						label="泛酸(毫克)">
						<template slot-scope="scope">
							{{scope.row.fanshuan}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="shenwushu"
						label="生物素(微克)">
						<template slot-scope="scope">
							{{scope.row.shenwushu}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="danjian"
						label="胆碱(毫克)">
						<template slot-scope="scope">
							{{scope.row.danjian}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="jinshulin"
						label="磷(毫克)">
						<template slot-scope="scope">
							{{scope.row.jinshulin}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="jinshujia"
						label="钾(毫克)">
						<template slot-scope="scope">
							{{scope.row.jinshujia}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="jinshumei"
						label="镁(毫克)">
						<template slot-scope="scope">
							{{scope.row.jinshumei}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="jinshugai"
						label="钙(毫克)">
						<template slot-scope="scope">
							{{scope.row.jinshugai}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="jinshutie"
						label="铁(毫克)">
						<template slot-scope="scope">
							{{scope.row.jinshutie}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="jinshuxin"
						label="锌(毫克)">
						<template slot-scope="scope">
							{{scope.row.jinshuxin}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="jinshudian"
						label="碘(微克)">
						<template slot-scope="scope">
							{{scope.row.jinshudian}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="jinshudxi"
						label="硒(微克)">
						<template slot-scope="scope">
							{{scope.row.jinshudxi}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="jinshutong"
						label="铜(毫克)">
						<template slot-scope="scope">
							{{scope.row.jinshutong}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="jinshufu"
						label="氟(毫克)">
						<template slot-scope="scope">
							{{scope.row.jinshufu}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="jinshumeng"
						label="锰(毫克)">
						<template slot-scope="scope">
							{{scope.row.jinshumeng}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="deltae"
						label="δ-E(毫克)">
						<template slot-scope="scope">
							{{scope.row.deltae}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="beitae"
						label="(β-γ)-E(毫克)">
						<template slot-scope="scope">
							{{scope.row.beitae}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="aerfae"
						label="α-E(毫克)">
						<template slot-scope="scope">
							{{scope.row.aerfae}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="hulubo"
						label="胡萝卜素(微克)">
						<template slot-scope="scope">
							{{scope.row.hulubo}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="zhifansz"
						label="脂肪酸（总）(克)">
						<template slot-scope="scope">
							{{scope.row.zhifansz}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="huifen"
						label="灰分(克)">
						<template slot-scope="scope">
							{{scope.row.huifen}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="shuifen"
						label="水分(克)">
						<template slot-scope="scope">
							{{scope.row.shuifen}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="nengliangqk"
						label="能量(千卡)">
						<template slot-scope="scope">
							{{scope.row.nengliangqk}}
						</template>
					</el-table-column>
					<el-table-column :resizable='true' :sortable='true'  
						prop="storeupnum"
						label="收藏数">
						<template slot-scope="scope">
							{{scope.row.storeupnum}}
						</template>
					</el-table-column>
					<el-table-column width="300" label="操作">
						<template slot-scope="scope">
							<el-button class="view" v-if=" isAuth('eshianyycf','查看')" type="success" @click="addOrUpdateHandler(scope.row.id,'info')">
								<span class="icon iconfont icon-xihuan" :style='{"margin":"0 2px","fontSize":"14px","color":"#fff","display":"none","height":"40px"}'></span>
								查看
							</el-button>
							<el-button class="edit" v-if=" isAuth('eshianyycf','修改') " type="success" @click="addOrUpdateHandler(scope.row.id)">
								<span class="icon iconfont icon-xihuan" :style='{"margin":"0 2px","fontSize":"14px","color":"#fff","display":"none","height":"40px"}'></span>
								修改
							</el-button>




							<el-button class="del" v-if="isAuth('eshianyycf','删除') " type="primary" @click="deleteHandler(scope.row.id )">
								<span class="icon iconfont icon-xihuan" :style='{"margin":"0 2px","fontSize":"14px","color":"#fff","display":"none","height":"40px"}'></span>
								删除
							</el-button>
						</template>
					</el-table-column>
				</el-table>
			</div>
			<el-pagination
				@size-change="sizeChangeHandle"
				@current-change="currentChangeHandle"
				:current-page="pageIndex"
				background
				:page-sizes="[10, 50, 100, 200]"
				:page-size="pageSize"
				:layout="layouts.join()"
				:total="totalPage"
				prev-text="< "
				next-text="> "
				:hide-on-single-page="false"
				:style='{"padding":"0","boxShadow":"none","margin":"20px auto 0","whiteSpace":"nowrap","color":"#333","alignItems":"center","textAlign":"center","display":"flex","justifyContent":"space-between","borderRadius":"5px  5px  5px  5px","background":"none","width":"500px","fontSize":"inherit","position":"relative","fontWeight":"500","height":"30px"}'
			></el-pagination>
		</template>
		
		<!-- 添加/修改页面  将父组件的search方法传递给子组件-->
		<add-or-update v-if="addOrUpdateFlag" :parent="this" ref="addOrUpdate"></add-or-update>




		<el-dialog
			:visible.sync="chartVisiable1"
			width="800">
			<div id="cnameChart1" style="width:100%;height:600px;"></div>
			<span slot="footer" class="dialog-footer">
				<el-button @click="chartDialog1">返回</el-button>
			</span>
		</el-dialog>
		<el-dialog
			:visible.sync="chartVisiable2"
			width="800">
			<div id="spfenleiChart2" style="width:100%;height:600px;"></div>
			<span slot="footer" class="dialog-footer">
				<el-button @click="chartDialog2">返回</el-button>
			</span>
		</el-dialog>
		<el-dialog
			:visible.sync="chartVisiable3"
			width="800">
			<div id="chandiChart3" style="width:100%;height:600px;"></div>
			<span slot="footer" class="dialog-footer">
				<el-button @click="chartDialog3">返回</el-button>
			</span>
		</el-dialog>
		<el-dialog
			:visible.sync="chartVisiable4"
			width="800">
			<div id="nengliangChart4" style="width:100%;height:600px;"></div>
			<span slot="footer" class="dialog-footer">
				<el-button @click="chartDialog4">返回</el-button>
			</span>
		</el-dialog>
		<el-dialog
			:visible.sync="chartVisiable5"
			width="800">
			<div id="danbaizhiChart5" style="width:100%;height:600px;"></div>
			<span slot="footer" class="dialog-footer">
				<el-button @click="chartDialog5">返回</el-button>
			</span>
		</el-dialog>
		<el-dialog
			:visible.sync="chartVisiable6"
			width="800">
			<div id="tshhwChart6" style="width:100%;height:600px;"></div>
			<span slot="footer" class="dialog-footer">
				<el-button @click="chartDialog6">返回</el-button>
			</span>
		</el-dialog>

	</div>
</template>

<script>
	import * as echarts from 'echarts'
	import chinaJson from "@/components/echarts/china.json";
	import axios from 'axios';
	import AddOrUpdate from "./add-or-update";
	import {
		Loading
	} from 'element-ui';
	export default {
		data() {
			return {
				indexQueryCondition: '',
				searchForm: {
					key: ""
				},
				form:{},
				dataList: [],
				pageIndex: 1,
				pageSize: 10,
				totalPage: 0,
				dataListLoading: false,
				dataListSelections: [],
				showFlag: true,
				chartVisiable1: false,
				line: {"backgroundColor":"transparent","yAxis":{"axisLabel":{"borderType":"solid","rotate":0,"padding":0,"shadowOffsetX":0,"margin":15,"backgroundColor":"transparent","borderColor":"#000","shadowOffsetY":0,"color":"#333","shadowBlur":0,"show":true,"inside":false,"ellipsis":"...","overflow":"none","borderRadius":0,"borderWidth":0,"width":"","fontSize":12,"lineHeight":24,"shadowColor":"transparent","fontWeight":"normal","height":""},"axisTick":{"show":true,"length":5,"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"cap":"butt","color":"#333","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"rgba(0,0,0,.5)"},"inside":false},"splitLine":{"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"cap":"butt","color":"#666","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"rgba(0,0,0,.5)"},"show":true},"axisLine":{"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"cap":"butt","color":"#333","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"rgba(0,0,0,.5)"},"show":true},"splitArea":{"show":false,"areaStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"color":"rgba(25,25,25,0.3)","opacity":1,"shadowBlur":10,"shadowColor":"rgba(0,0,0,.5)"}}},"xAxis":{"axisLabel":{"borderType":"solid","rotate":0,"padding":0,"shadowOffsetX":0,"margin":4,"backgroundColor":"transparent","borderColor":"#000","shadowOffsetY":0,"color":"#333","shadowBlur":0,"show":true,"inside":false,"ellipsis":"...","overflow":"none","borderRadius":0,"borderWidth":0,"width":"","fontSize":12,"lineHeight":24,"shadowColor":"transparent","fontWeight":"normal","height":""},"axisTick":{"show":true,"length":5,"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"cap":"butt","color":"#333","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"rgba(0,0,0,.5)"},"inside":false},"splitLine":{"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"cap":"butt","color":"#333","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"rgba(0,0,0,.5)"},"show":false},"axisLine":{"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"cap":"butt","color":"#333","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"rgba(0,0,0,.5)"},"show":true},"splitArea":{"show":false,"areaStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"color":"rgba(25,25,25,.3)","opacity":1,"shadowBlur":10,"shadowColor":"rgba(0,0,0,.5)"}}},"color":["#5DCEFC","#91cc75","#fac858","#ee6666","#73c0de","#3ba272","#fc8452","#9a60b4","#ea7ccc"],"legend":{"padding":0,"itemGap":10,"shadowOffsetX":0,"backgroundColor":"transparent","borderColor":"#666","shadowOffsetY":0,"orient":"horizontal","shadowBlur":0,"bottom":"auto","itemHeight":14,"show":true,"icon":"roundRect","itemStyle":{"borderType":"solid","shadowOffsetX":0,"borderColor":"inherit","shadowOffsetY":0,"color":"#333","shadowBlur":0,"borderWidth":0,"opacity":1,"shadowColor":"transparent"},"right":"auto","top":"auto","borderRadius":0,"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"color":"inherit","shadowBlur":0,"width":"auto","type":"inherit","opacity":1,"shadowColor":"transparent"},"left":"right","borderWidth":0,"width":"80%","itemWidth":20,"textStyle":{"textBorderWidth":0,"color":"#333","textShadowColor":"transparent","ellipsis":"...","overflow":"none","fontSize":12,"lineHeight":24,"textShadowOffsetX":0,"textShadowOffsetY":0,"textBorderType":"solid","fontWeight":500,"textBorderColor":"transparent","textShadowBlur":0},"shadowColor":"rgba(0,0,0,.3)","height":"auto"},"series":{"showSymbol":true,"symbol":"emptyCircle","symbolSize":4},"tooltip":{"backgroundColor":"#123","textStyle":{"color":"#fff"}},"title":{"borderType":"solid","padding":0,"shadowOffsetX":0,"backgroundColor":"transparent","borderColor":"#666","shadowOffsetY":0,"shadowBlur":0,"bottom":"auto","show":true,"right":"auto","top":"auto","borderRadius":0,"left":"left","borderWidth":0,"textStyle":{"textBorderWidth":0,"color":"#333","textShadowColor":"transparent","fontSize":14,"lineHeight":24,"textShadowOffsetX":0,"textShadowOffsetY":0,"textBorderType":"solid","fontWeight":600,"textBorderColor":"#666","textShadowBlur":0},"shadowColor":"transparent"}},
				bar: {"backgroundColor":"transparent","yAxis":{"axisLabel":{"borderType":"solid","rotate":0,"padding":0,"shadowOffsetX":0,"margin":12,"backgroundColor":"transparent","borderColor":"#666","shadowOffsetY":0,"color":"#333","shadowBlur":0,"show":true,"inside":false,"ellipsis":"...","overflow":"none","borderRadius":0,"borderWidth":0,"width":"","fontSize":12,"lineHeight":24,"shadowColor":"transparent","fontWeight":"normal","height":""},"axisTick":{"show":true,"length":5,"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"cap":"butt","color":"#348cb4","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"#348cb4)"},"inside":false},"splitLine":{"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"cap":"butt","color":"#666","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"rgba(0,0,0,.5)"},"show":true},"axisLine":{"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"cap":"butt","color":"#348cb4","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"#348cb4"},"show":true},"splitArea":{"show":false,"areaStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"color":"rgba(25,25,25,0.3)","opacity":1,"shadowBlur":10,"shadowColor":"rgba(0,0,0,.5)"}}},"xAxis":{"axisLabel":{"borderType":"solid","rotate":0,"padding":0,"shadowOffsetX":0,"margin":4,"backgroundColor":"transparent","borderColor":"#000","shadowOffsetY":0,"color":"#348cb4","shadowBlur":0,"show":true,"inside":false,"ellipsis":"...","overflow":"none","borderRadius":0,"borderWidth":0,"width":"","fontSize":12,"lineHeight":24,"shadowColor":"transparent","fontWeight":"normal","height":""},"axisTick":{"show":true,"length":5,"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"cap":"butt","color":"#348cb4","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"rgba(0,0,0,.5)"},"inside":false},"splitLine":{"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"cap":"butt","color":"#348cb4","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"rgba(0,0,0,.5)"},"show":false},"axisLine":{"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"cap":"butt","color":"#348cb4","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"rgba(0,0,0,.5)"},"show":true},"splitArea":{"show":false,"areaStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"color":"#348cb4","opacity":1,"shadowBlur":10,"shadowColor":"#348cb4"}}},"color":["#55a7bf","#55a7bf","#55a7bf","#55a7bf","#55a7bf","#55a7bf","#55a7bf","#55a7bf"],"legend":{"padding":0,"itemGap":10,"shadowOffsetX":0,"backgroundColor":"transparent","borderColor":"#666","shadowOffsetY":0,"orient":"horizontal","shadowBlur":0,"bottom":"auto","itemHeight":14,"show":true,"icon":"roundRect","itemStyle":{"borderType":"solid","shadowOffsetX":0,"borderColor":"inherit","shadowOffsetY":0,"color":"#333","shadowBlur":0,"borderWidth":0,"opacity":1,"shadowColor":"transparent"},"right":"auto","top":"auto","borderRadius":0,"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"color":"inherit","shadowBlur":0,"width":"auto","type":"inherit","opacity":1,"shadowColor":"transparent"},"left":"right","borderWidth":0,"width":"80%","itemWidth":20,"textStyle":{"textBorderWidth":0,"color":"inherit","textShadowColor":"transparent","ellipsis":"...","overflow":"none","fontSize":12,"lineHeight":12,"textShadowOffsetX":0,"textShadowOffsetY":0,"textBorderType":"solid","fontWeight":500,"textBorderColor":"transparent","textShadowBlur":0},"shadowColor":"rgba(0,0,0,.3)","height":"auto"},"series":{"barWidth":"auto","itemStyle":{"borderType":"solid","shadowOffsetX":0,"borderColor":"#666","shadowOffsetY":0,"color":"","shadowBlur":0,"borderWidth":0,"opacity":1,"shadowColor":"#000"},"colorBy":"data","barCategoryGap":"20%"},"tooltip":{"backgroundColor":"#123","textStyle":{"color":"#fff"}},"title":{"borderType":"solid","padding":0,"shadowOffsetX":0,"backgroundColor":"transparent","borderColor":"#666","shadowOffsetY":0,"shadowBlur":0,"bottom":"auto","show":true,"right":"auto","top":"auto","borderRadius":0,"left":"center","borderWidth":0,"textStyle":{"textBorderWidth":0,"color":"#55a7bf","textShadowColor":"transparent","fontSize":14,"lineHeight":24,"textShadowOffsetX":0,"textShadowOffsetY":0,"textBorderType":"solid","fontWeight":600,"textBorderColor":"#666","textShadowBlur":0},"shadowColor":"transparent"},"base":{"animate":false,"interval":2000}},
				pie: {"tooltip":{"backgroundColor":"#123","textStyle":{"color":"#fff"}},"backgroundColor":"transparent","color":["#ee6666","#73c0de","#3ba272","#fc8452","#9a60b4","#ea7ccc","green","pink","red"],"title":{"borderType":"solid","padding":0,"shadowOffsetX":0,"backgroundColor":"transparent","borderColor":"#666","shadowOffsetY":0,"shadowBlur":0,"bottom":"auto","show":true,"right":"auto","top":"auto","borderRadius":0,"left":"center","borderWidth":0,"textStyle":{"textBorderWidth":0,"color":"#55a7bf","textShadowColor":"transparent","fontSize":14,"lineHeight":14,"textShadowOffsetX":0,"textShadowOffsetY":0,"textBorderType":"solid","fontWeight":600,"textBorderColor":"#666","textShadowBlur":0},"shadowColor":"transparent"},"legend":{"padding":0,"itemGap":10,"shadowOffsetX":0,"backgroundColor":"transparent","borderColor":"#666","shadowOffsetY":0,"orient":"vertical","shadowBlur":0,"bottom":"auto","itemHeight":2,"show":true,"icon":"roundRect","itemStyle":{"borderType":"solid","shadowOffsetX":0,"borderColor":"inherit","shadowOffsetY":0,"color":"inherit","shadowBlur":0,"borderWidth":0,"opacity":1,"shadowColor":"transparent"},"right":100,"top":"auto","borderRadius":0,"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"color":"inherit","shadowBlur":0,"width":"auto","type":"inherit","opacity":1,"shadowColor":"transparent"},"left":"right","borderWidth":0,"width":"80%","itemWidth":8,"textStyle":{"textBorderWidth":0,"color":"inherit","textShadowColor":"transparent","ellipsis":"...","overflow":"none","fontSize":12,"lineHeight":12,"textShadowOffsetX":0,"textShadowOffsetY":0,"textBorderType":"solid","fontWeight":500,"textBorderColor":"transparent","textShadowBlur":0},"shadowColor":"rgba(0,0,0,.3)","height":"auto"},"series":{"itemStyle":{"borderType":"solid","shadowOffsetX":0,"borderColor":"#666","shadowOffsetY":0,"color":"","shadowBlur":0,"borderWidth":0,"opacity":1,"shadowColor":"#000"},"label":{"borderType":"solid","rotate":0,"padding":0,"textBorderWidth":0,"backgroundColor":"transparent","borderColor":"#666","color":"inherit","show":true,"textShadowColor":"transparent","distanceToLabelLine":5,"ellipsis":"...","overflow":"none","borderRadius":0,"borderWidth":0,"fontSize":12,"lineHeight":18,"textShadowOffsetX":0,"position":"outside","textShadowOffsetY":0,"textBorderType":"solid","textBorderColor":"#666","textShadowBlur":0},"labelLine":{"show":true,"length":10,"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"color":"#666","shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"#000"},"length2":14,"smooth":false}}},
				funnel: {"tooltip":{"backgroundColor":"#123","textStyle":{"color":"#fff"}},"backgroundColor":"transparent","color":["#91CC75","#91cc75","#fac858","#ee6666","#73c0de","#3ba272","#fc8452","#9a60b4","#ea7ccc"],"title":{"borderType":"solid","padding":2,"shadowOffsetX":0,"backgroundColor":"transparent","borderColor":"#ccc","shadowOffsetY":0,"shadowBlur":0,"bottom":"auto","show":true,"right":"auto","top":"auto","borderRadius":0,"left":"center","borderWidth":0,"textStyle":{"textBorderWidth":0,"color":"#666","textShadowColor":"transparent","fontSize":14,"lineHeight":12,"textShadowOffsetX":0,"textShadowOffsetY":0,"textBorderType":"solid","fontWeight":500,"textBorderColor":"#ccc","textShadowBlur":0},"shadowColor":"transparent"},"legend":{"padding":5,"itemGap":10,"shadowOffsetX":0,"backgroundColor":"transparent","borderColor":"#ccc","shadowOffsetY":0,"orient":"vertical","shadowBlur":0,"bottom":"auto","itemHeight":2,"show":true,"icon":"roundRect","itemStyle":{"borderType":"solid","shadowOffsetX":0,"borderColor":"inherit","shadowOffsetY":0,"color":"inherit","shadowBlur":0,"borderWidth":0,"opacity":1,"shadowColor":"transparent"},"top":"auto","borderRadius":0,"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"color":"inherit","shadowBlur":0,"width":"auto","type":"inherit","opacity":1,"shadowColor":"transparent"},"left":"left","borderWidth":0,"width":"auto","itemWidth":2,"textStyle":{"textBorderWidth":0,"color":"inherit","textShadowColor":"transparent","ellipsis":"...","overflow":"none","fontSize":12,"lineHeight":20,"textShadowOffsetX":0,"textShadowOffsetY":0,"textBorderType":"solid","fontWeight":500,"textBorderColor":"transparent","textShadowBlur":0},"shadowColor":"rgba(0,0,0,.3)","height":"auto"},"series":{"itemStyle":{"borderType":"solid","shadowOffsetX":0,"borderColor":"#000","shadowOffsetY":0,"color":"","shadowBlur":0,"borderWidth":0,"opacity":1,"shadowColor":"#000"},"label":{"borderType":"solid","rotate":0,"padding":0,"textBorderWidth":0,"backgroundColor":"transparent","borderColor":"#fff","color":"","show":true,"textShadowColor":"transparent","distanceToLabelLine":5,"ellipsis":"...","overflow":"none","borderRadius":0,"borderWidth":0,"fontSize":12,"lineHeight":18,"textShadowOffsetX":0,"position":"outside","textShadowOffsetY":0,"textBorderType":"solid","textBorderColor":"#fff","textShadowBlur":0},"labelLine":{"show":true,"length":10,"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"shadowBlur":0,"width":1,"type":"solid","opacity":1,"shadowColor":"#000"},"length2":14,"smooth":false}}},
				boardBase: {"funnelNum":8,"lineNum":8,"gaugeNum":8,"barNum":8,"pieNum":8},
				gauge: {"tooltip":{"backgroundColor":"#123","textStyle":{"color":"#fff"}},"backgroundColor":"transparent","color":["#38669F","#91cc75","#fac858","#ee6666","#73c0de","#3ba272","#fc8452","#9a60b4","#ea7ccc"],"title":{"top":"top","left":"left","textStyle":{"fontSize":14,"lineHeight":24,"color":"#333","fontWeight":600}},"series":{"pointer":{"offsetCenter":[0,"10%"],"icon":"path://M2.9,0.7L2.9,0.7c1.4,0,2.6,1.2,2.6,2.6v115c0,1.4-1.2,2.6-2.6,2.6l0,0c-1.4,0-2.6-1.2-2.6-2.6V3.3C0.3,1.9,1.4,0.7,2.9,0.7z","width":8,"length":"80%"},"axisLine":{"lineStyle":{"shadowOffsetX":0,"shadowOffsetY":0,"opacity":0.5,"shadowBlur":1,"shadowColor":"#000"},"roundCap":true},"anchor":{"show":true,"itemStyle":{"color":"inherit"},"size":18,"showAbove":true},"emphasis":{"disabled":false},"progress":{"show":true,"roundCap":true,"overlap":true},"splitNumber":25,"detail":{"formatter":"{value}","backgroundColor":"inherit","color":"#fff","borderRadius":3,"width":20,"fontSize":12,"height":10},"title":{"fontSize":14},"animation":true}},
				chartVisiable2: false,
				chartVisiable3: false,
				chartVisiable4: false,
				chartVisiable5: false,
				chartVisiable6: false,
				addOrUpdateFlag:false,
				layouts: ["total","prev","pager","next","sizes"],
			};
		},
		created() {
			this.init();
			this.getDataList();
			this.contentStyleChange();
		},
		mounted() {
		},
		filters: {
			htmlfilter: function (val) {
				return val.replace(/<[^>]*>/g).replace(/undefined/g,'');
			}
		},
		computed: {
			tablename(){
				return this.$storage.get('sessionTable')
			},
		},
		components: {
			AddOrUpdate,
		},
		methods: {
			linkOthers(url) {
				window.open(url);//打开一个新的标签页
			},
			contentStyleChange() {
				this.contentPageStyleChange()
			},
			// 分页
			contentPageStyleChange(){
				let arr = []

				// if(this.contents.pageTotal) arr.push('total')
				// if(this.contents.pageSizes) arr.push('sizes')
				// if(this.contents.pagePrevNext){
				//   arr.push('prev')
				//   if(this.contents.pagePager) arr.push('pager')
				//   arr.push('next')
				// }
				// if(this.contents.pageJumper) arr.push('jumper')
				// this.layouts = arr.join()
				// this.contents.pageEachNum = 10
			},


			// 统计接口
			chartDialog1() {
				this.chartVisiable1 = !this.chartVisiable1;
				this.$nextTick(()=>{
					var cnameChart1 = echarts.init(document.getElementById("cnameChart1"),'macarons');
					this.$http({
						url: "eshianyycf/group/cname",
						method: "get",
					}).then(({ data }) => {
						if (data && data.code === 0) {
							let res = data.data;
							let xAxis = [];
							let yAxis = [];
							let pArray = []
							for(let i=0;i<res.length;i++){
								xAxis.push(res[i].cname);
								yAxis.push(parseFloat((res[i].total)));
								pArray.push({
									value: parseFloat((res[i].total)),
									name: res[i].cname
								})
							}
							var option = {};
							// 使用刚指定的配置项和数据显示图表。
							cnameChart1.setOption(option);
							  //根据窗口的大小变动图表
							window.onresize = function() {
								cnameChart1.resize();
							};
						}else{
							this.$message({
								message: data.msg,
								type: "warning",
								duration: 1500,
							})
						}
					});
				})
			},

			// 统计接口
			chartDialog2() {
				this.chartVisiable2 = !this.chartVisiable2;
				this.$nextTick(()=>{

					var spfenleiChart2 = echarts.init(document.getElementById("spfenleiChart2"),'macarons');
					this.$http({
						url: "eshianyycf/group/spfenlei",
						method: "get",
					}).then(({ data }) => {
						if (data && data.code === 0) {
							let res = data.data;
							let xAxis = [];
							let yAxis = [];
							let pArray = []
							for(let i=0;i<res.length;i++){
								if(this.boardBase&&i==this.boardBase.pieNum){
									break;
								}
								xAxis.push(res[i].spfenlei);
								yAxis.push(parseFloat((res[i].total)));
								pArray.push({
									value: parseFloat((res[i].total)),
									name: res[i].spfenlei
								})
							}
							var option = {};
							let titleObj = this.pie.title
							titleObj.text = '食物类型分布'
							
							const legendObj = this.pie.legend
							let tooltipObj = {trigger: 'item',formatter: '{b} : {c} ({d}%)'}
							tooltipObj = Object.assign(tooltipObj , this.pie.tooltip?this.pie.tooltip:{})
							
							let seriesObj = {
								type: 'pie',
								radius: '55%',
								center: ['50%', '60%'],
								data: pArray,
								emphasis: {
									itemStyle: {
										shadowBlur: 10,
										shadowOffsetX: 0,
										shadowColor: 'rgba(0, 0, 0, 0.5)'
									}
								}
							}
							seriesObj = Object.assign(seriesObj , this.pie.series)
							const gridObj = this.pie.grid
							option = {
								backgroundColor: this.pie.backgroundColor,
								color: this.pie.color,
								title: titleObj,
								legend: legendObj,
								tooltip: tooltipObj,
								series: [seriesObj],
								grid: gridObj
							};
							// 使用刚指定的配置项和数据显示图表。
							spfenleiChart2.setOption(option);
							//根据窗口的大小变动图表
							window.onresize = function() {
								spfenleiChart2.resize();
							};
						}else{
							this.$message({
								message: data.msg,
								type: "warning",
								duration: 1500,
							})
						}
					});
				})
			},

			// 统计接口
			chartDialog3() {
				this.chartVisiable3 = !this.chartVisiable3;
				this.$nextTick(()=>{

					var chandiChart3 = echarts.init(document.getElementById("chandiChart3"),'macarons');
					this.$http({
						url: "eshianyycf/group/chandi",
						method: "get",
					}).then(({ data }) => {
						if (data && data.code === 0) {
							let res = data.data;
							let xAxis = [];
							let yAxis = [];
							let pArray = []
							for(let i=0;i<res.length;i++){
								if(this.boardBase&&i==this.boardBase.barNum){
									break;
								}
								xAxis.push(res[i].chandi);
								yAxis.push(parseFloat((res[i].total)));
								pArray.push({
									value: parseFloat((res[i].total)),
									name: res[i].chandi
								})
							}
							var option = {};
							let titleObj = this.bar.title
							titleObj.text = '产地分布'
							
							const legendObj = this.bar.legend
							let tooltipObj = {trigger: 'item',formatter: '{b} : {c}'}
							tooltipObj = Object.assign(tooltipObj , this.bar.tooltip?this.bar.tooltip:{})
				
							let xAxisObj = this.bar.xAxis
							xAxisObj.type = 'category'
							xAxisObj.data = xAxis
							
							let yAxisObj = this.bar.yAxis
							yAxisObj.type = 'value'
				
							let seriesObj = {
								data: yAxis,
								type: 'bar',
							}
							seriesObj = Object.assign(seriesObj , this.bar.series)
							const gridObj = this.bar.grid
							option = {
								backgroundColor: this.bar.backgroundColor,
								color: this.bar.color,
								title: titleObj,
								legend: legendObj,
								tooltip: tooltipObj,
								xAxis: xAxisObj,
								yAxis: yAxisObj,
								series: [seriesObj],
								grid: gridObj
							};
							// 使用刚指定的配置项和数据显示图表。
							chandiChart3.setOption(option);
							//根据窗口的大小变动图表
							window.onresize = function() {
								chandiChart3.resize();
							};
						}else{
							this.$message({
								message: data.msg,
								type: "warning",
								duration: 1500,
							})
						}
					});
				})
			},

			// 统计接口
			chartDialog4() {
				this.chartVisiable4 = !this.chartVisiable4;
				this.$nextTick(()=>{

					var nengliangChart4 = echarts.init(document.getElementById("nengliangChart4"),'macarons');
					this.$http({
						url: "eshianyycf/sectionStat/nengliang",
						method: "get",
					}).then(({ data }) => {
						if (data && data.code === 0) {
							let res = data.data;
							let xAxis = [];
							let yAxis = [];
							let pArray = []
							for(let i=0;i<res.length;i++){
								if(this.boardBase&&i==this.boardBase.pieNum){
									break;
								}
								xAxis.push(res[i].nengliang);
								yAxis.push(parseFloat((res[i].total)));
								pArray.push({
									value: parseFloat((res[i].total)),
									name: res[i].nengliang
								})
							}
							var option = {};
							let titleObj = this.pie.title
							titleObj.text = '能量区间'
							
							const legendObj = this.pie.legend
							let tooltipObj = {trigger: 'item',formatter: '{b} : {c} ({d}%)'}
							tooltipObj = Object.assign(tooltipObj , this.pie.tooltip?this.pie.tooltip:{})
							
							let seriesObj = {
								type: 'pie',
								radius: ['25%', '55%'],
								center: ['50%', '60%'],
								data: pArray,
								emphasis: {
									itemStyle: {
										shadowBlur: 10,
										shadowOffsetX: 0,
										shadowColor: 'rgba(0, 0, 0, 0.5)'
									}
								}
							}
							seriesObj = Object.assign(seriesObj , this.pie.series)
							const gridObj = this.bar.grid
							option = {
								backgroundColor: this.pie.backgroundColor,
								color: this.pie.color,
								title: titleObj,
								legend: legendObj,
								tooltip: tooltipObj,
								series: [seriesObj],
								grid: gridObj
							};
							// 使用刚指定的配置项和数据显示图表。
							nengliangChart4.setOption(option);
							//根据窗口的大小变动图表
							window.onresize = function() {
								nengliangChart4.resize();
							};
						}else{
							this.$message({
								message: data.msg,
								type: "warning",
								duration: 1500,
							})
						}
					});
				})
			},
			// 统计接口
			chartDialog5() {
				this.chartVisiable5 = !this.chartVisiable5;
				this.$nextTick(()=>{

					var danbaizhiChart5 = echarts.init(document.getElementById("danbaizhiChart5"),'macarons');
					this.$http({
						url: `eshianyycf/value/cname/danbaizhi`,
						method: "get",
					}).then(({ data }) => {
						if (data && data.code === 0) {
							let res = data.data;
							let xAxis = [];
							let yAxis = [];
							let pArray = []
							for(let i=0;i<res.length;i++){
								if(this.boardBase&&i==this.boardBase.barNum){
									break;
								}
								xAxis.push(res[i].cname);
								yAxis.push(parseFloat((res[i].total)));
								pArray.push({
									value: parseFloat((res[i].total)),
									name: res[i].cname
								})
							}
							var option = {};
							let titleObj = this.bar.title
							titleObj.text = '蛋白质排名'
							
							const legendObj = this.bar.legend
							
							let tooltipObj = {trigger: 'item',formatter: '{b} : {c}'}
							tooltipObj = Object.assign(tooltipObj , this.bar.tooltip?this.bar.tooltip:{})
							let xAxisObj = this.bar.xAxis
							xAxisObj.type = 'value'
							
							let yAxisObj = this.bar.yAxis
							yAxisObj.type = 'category'
							yAxisObj.data = xAxis
				
							let seriesObj = {
								data: yAxis,
								type: 'bar',
							}
							seriesObj = Object.assign(seriesObj , this.bar.series)
							const gridObj = this.bar.grid
							option = {
								backgroundColor: this.bar.backgroundColor,
								color: this.bar.color,
								title: titleObj,
								legend: legendObj,
								tooltip: tooltipObj,
								xAxis: xAxisObj,
								yAxis: yAxisObj,
								series: [seriesObj],
								grid: gridObj
							};
							// 使用刚指定的配置项和数据显示图表。
							danbaizhiChart5.setOption(option);
							//根据窗口的大小变动图表
							window.onresize = function() {
								danbaizhiChart5.resize();
							};
						}else{
							this.$message({
								message: data.msg,
								type: "warning",
								duration: 1500,
							})
						}
					});
				})
			},
			// 统计接口
			chartDialog6() {
				this.chartVisiable6 = !this.chartVisiable6;
				this.$nextTick(()=>{

					var tshhwChart6 = echarts.init(document.getElementById("tshhwChart6"),'macarons');
					this.$http({
						url: `eshianyycf/value/cname/tshhw`,
						method: "get",
					}).then(({ data }) => {
						if (data && data.code === 0) {
							let res = data.data;
							let xAxis = [];
							let yAxis = [];
							let pArray = []
							for(let i=0;i<res.length;i++){
								if(this.boardBase&&i==this.boardBase.lineNum){
									break;
								}
								xAxis.push(res[i].cname);
								yAxis.push(parseFloat((res[i].total)));
								pArray.push({
									value: parseFloat((res[i].total)),
									name: res[i].cname
								})
							}
							var option = {};
							let titleObj = this.line.title
							titleObj.text = '碳水化合物排名'
							
							const legendObj = this.line.legend
							let tooltipObj = { trigger: 'item',formatter: '{b} : {c}'}
							tooltipObj = Object.assign(tooltipObj , this.line.tooltip?this.line.tooltip:{})
							
							let xAxisObj = this.line.xAxis
							xAxisObj.type = 'category'
							xAxisObj.boundaryGap = false
							xAxisObj.data = xAxis
							
							let yAxisObj = this.line.yAxis
							yAxisObj.type = 'value'
							
							let seriesObj = {
								data: yAxis,
								type: 'line',
							}
							seriesObj = Object.assign(seriesObj , this.line.series)
							const gridObj = this.line.grid
							option = {
								backgroundColor: this.line.backgroundColor,
								color: this.line.color,
								title: titleObj,
								legend: legendObj,
								tooltip: tooltipObj,
								xAxis: xAxisObj,
								yAxis: yAxisObj,
								series: [seriesObj],
								grid: gridObj
							};
							// 使用刚指定的配置项和数据显示图表。
							tshhwChart6.setOption(option);
							//根据窗口的大小变动图表
							window.onresize = function() {
								tshhwChart6.resize();
							};
						}else{
							this.$message({
								message: data.msg,
								type: "warning",
								duration: 1500,
							})
						}
					});
				})
			},
			init () {
			},
			search() {
				this.pageIndex = 1;
				this.getDataList();
			},

			// 获取数据列表
			getDataList() {
				this.dataListLoading = true;
				let params = {
					page: this.pageIndex,
					limit: this.pageSize,
					sort: 'id',
					order: 'desc',
				}
 				if(this.searchForm.cname!='' && this.searchForm.cname!=undefined){
					params['cname'] = '%' + this.searchForm.cname + '%'
				}
 				if(this.searchForm.spfenlei!='' && this.searchForm.spfenlei!=undefined){
					params['spfenlei'] = '%' + this.searchForm.spfenlei + '%'
				}
 				if(this.searchForm.chandi!='' && this.searchForm.chandi!=undefined){
					params['chandi'] = '%' + this.searchForm.chandi + '%'
				}
				let user = JSON.parse(this.$storage.getObj('userForm'))
				this.$http({
					url: "eshianyycf/page",
					method: "get",
					params: params
				}).then(({ data }) => {
					if (data && data.code === 0) {
						this.dataList = data.data.list;
						this.totalPage = data.data.total;
					} else {
						this.dataList = [];
						this.totalPage = 0;
					}
					this.dataListLoading = false;
				});
			},
			// 每页数
			sizeChangeHandle(val) {
				this.pageSize = val;
				this.pageIndex = 1;
				this.getDataList();
			},
			// 当前页
			currentChangeHandle(val) {
				this.pageIndex = val;
				this.getDataList();
			},
			// 多选
			selectionChangeHandler(val) {
				this.dataListSelections = val;
			},
			// 添加/修改
			addOrUpdateHandler(id,type) {
				this.showFlag = false;
				this.addOrUpdateFlag = true;
				this.crossAddOrUpdateFlag = false;
				if(type!='info'&&type!='msg'){
					type = 'else';
				}
				this.$nextTick(() => {
					this.$refs.addOrUpdate.init(id,type);
				});
			},
			// 删除
			async deleteHandler(id ) {
				var ids = id? [Number(id)]: this.dataListSelections.map(item => {
					return Number(item.id);
				});
				await this.$confirm(`确定进行[${id ? "删除" : "批量删除"}]操作?`, "提示", {
					confirmButtonText: "确定",
					cancelButtonText: "取消",
					type: "warning"
				}).then(async () => {
					await this.$http({
						url: "eshianyycf/delete",
						method: "post",
						data: ids
					}).then(async ({ data }) => {
						if (data && data.code === 0) {
							for(let x in ids){
								await this.$http.get('storeup/list',{params: {
									page: 1,
									limit: 100,
									refid: ids[x],
									tablename: 'eshianyycf'
								}}).then(async obj=>{
									if(obj.data&&obj.data.code==0){
										if(obj.data.data.list.length){
											let arr = []
											for(let i in obj.data.data.list){
												arr.push(obj.data.data.list[i].id)
											}
											await this.$http.post('storeup/delete',arr).then(()=>{})
										}
									}
								})
							}
							this.$message({
								message: "操作成功",
								type: "success",
								duration: 1500,
								onClose: () => {
									this.search();
								}
							});
			
						} else {
							this.$message.error(data.msg);
						}
					});
				});
			},

			spider() {
				this.$message({
					message: "数据爬取中...",
					type: "success",
					duration: 3000,
					onClose: () => {
						this.search();
					}
				});
				this.$http({
					url: "spider/eshianyycf",
					method: "get",
				}).then(({ data }) => {
					if (data && data.code === 0) {
						this.$message({
							message: "爬取完成",
							type: "success",
							duration: 1500,
							onClose: () => {
								this.getDataList(this.roleName);
							}
						});
					} else {
						this.$alert(data.msg)
					}
				});
			},

		}

	};
</script>
<style lang="scss" scoped>
	
	.center-form-pv {
		.el-date-editor.el-input {
			width: auto;
		}
	}
	
	.el-input {
		width: auto;
	}
	
	// form
	.center-form-pv .el-input {
		width: 100%;
	}
	.center-form-pv .el-input /deep/ .el-input__inner {
		border: 2px solid #000000;
		border-radius: 5px;
		padding: 0 12px;
		color: #666;
		background: #F4F4F4;
		width: 170px;
		font-size: 14px;
		height: 40px;
	}
	.center-form-pv .el-select {
		width: 100%;
	}
	.center-form-pv .el-select /deep/ .el-input__inner {
		border: 2px solid #000000;
		border-radius: 5px;
		padding: 0 12px;
		color: #666;
		background: #F4F4F4;
		width: 170px;
		font-size: 14px;
		height: 40px;
	}
	.center-form-pv .el-date-editor {
		width: 100%;
	}
	
	.center-form-pv .el-date-editor /deep/ .el-input__inner {
		border: 2px solid #000000;
		border-radius: 5px;
		padding: 0 30px;
		color: #666;
		background: #F4F4F4;
		width: 170px;
		font-size: 14px;
		height: 40px;
	}
	
	.center-form-pv .search {
		border: 0;
		cursor: pointer;
		border-radius: 5px;
		padding: 0 10px;
		margin: 0 0px 10px 0;
		color: #fff;
		background: #66D5F8;
		width: auto;
		font-size: 16px;
		height: 40px;
	}
	
	.center-form-pv .search:hover {
		opacity: 0.8;
	}
	
	.center-form-pv .actions .add {
		border: 0px solid #ddd;
		cursor: pointer;
		border-radius: 5px 5px 5px 5px;
		padding: 0 10px;
		margin: 4px;
		color: #fff;
		background: #66D5F8;
		width: auto;
		font-size: inherit;
		height: 32px;
	}
	
	.center-form-pv .actions .add:hover {
		opacity: 0.8;
	}
	
	.center-form-pv .actions .del {
		border: 0px solid #ddd;
		cursor: pointer;
		border-radius: 5px 5px 5px 5px;
		padding: 0 10px;
		margin: 4px;
		color: #fff;
		background: #02A79C;
		width: auto;
		font-size: inherit;
		height: 32px;
	}
	
	.center-form-pv .actions .del:hover {
		opacity: 0.8;
	}
	
	.center-form-pv .actions .statis {
		border: 0px solid #ddd;
		cursor: pointer;
		border-radius: 2px;
		padding: 0 10px;
		margin: 4px;
		color: #fff;
		background: #3bc1ff;
		width: auto;
		font-size: inherit;
		height: 34px;
	}
	
	.center-form-pv .actions .statis:hover {
		opacity: 0.8;
	}
	
	.center-form-pv .actions .btn18 {
		border: 0px solid #ddd;
		cursor: pointer;
		border-radius: 2px;
		padding: 0 10px;
		margin: 4px;
		color: #fff;
		background: #EF8E6A;
		width: auto;
		font-size: inherit;
		height: 34px;
	}
	
	.center-form-pv .actions .btn18:hover {
		opacity: 0.8;
	}
	
	// table
	.el-table /deep/ .el-table__header-wrapper thead {
		color: #999;
		font-weight: 500;
		width: 100%;
	}
	
	.el-table /deep/ .el-table__header-wrapper thead tr {
		background: #fff;
	}
	
	.el-table /deep/ .el-table__header-wrapper thead tr th {
		padding: 4px 0;
		background: none;
		border-color: #eee;
		border-width: 0 0px 1px 0;
		border-style: solid;
		text-align: left;
	}

	.el-table /deep/ .el-table__header-wrapper thead tr th .cell {
		padding: 0 0 0 5px;
		word-wrap: normal;
		color: #666;
		white-space: normal;
		font-weight: bold;
		display: flex;
		vertical-align: middle;
		font-size: 14px;
		line-height: 24px;
		text-overflow: ellipsis;
		word-break: break-all;
		width: 100%;
		align-items: center;
		position: relative;
		min-width: 110px;
	}

	.el-table /deep/ .el-table__body-wrapper {
		position: relative;
	}
	.el-table /deep/ .el-table__body-wrapper tbody {
		width: 100%;
	}

	.el-table /deep/ .el-table__body-wrapper tbody tr {
		background: #fff;
	}
	
	.el-table /deep/ .el-table__body-wrapper tbody tr td {
		padding: 4px 0;
		color: #333;
		background: #fff;
		font-size: inherit;
		border-color: #eee;
		border-width: 0 0px 1px 0;
		border-style: solid;
		text-align: left;
	}
	
		.el-table /deep/ .el-table__body-wrapper tbody tr.el-table__row--striped td {
		background: #f8f8f8;
	}
		
	.el-table /deep/ .el-table__body-wrapper tbody tr:hover td {
		padding: 4px 0;
		color: #333;
		background: #f0f0f0;
		border-color: #eee;
		border-width: 0 0px 1px 0;
		border-style: solid;
		text-align: left;
	}
	
	.el-table /deep/ .el-table__body-wrapper tbody tr td {
		padding: 4px 0;
		color: #333;
		background: #fff;
		font-size: inherit;
		border-color: #eee;
		border-width: 0 0px 1px 0;
		border-style: solid;
		text-align: left;
	}

	.el-table /deep/ .el-table__body-wrapper tbody tr td .cell {
		padding: 0 0 0 5px;
		overflow: hidden;
		word-break: break-all;
		white-space: normal;
		font-size: inherit;
		line-height: 24px;
		text-overflow: ellipsis;
	}
	
	.el-table /deep/ .el-table__body-wrapper tbody tr td .view {
		border: 0px solid #157ed2;
		cursor: pointer;
		border-radius: 2px;
		padding: 0 10px;
		margin: 0 5px 5px 0;
		color: #fff;
		background: #157ed2;
		width: auto;
		font-size: 14px;
		height: 32px;
	}
	
	.el-table /deep/ .el-table__body-wrapper tbody tr td .view:hover {
		opacity: 0.8;
	}
	
	.el-table /deep/ .el-table__body-wrapper tbody tr td .add {
	}
	
	.el-table /deep/ .el-table__body-wrapper tbody tr td .add:hover {
	}
	
	.el-table /deep/ .el-table__body-wrapper tbody tr td .edit {
		border: 0px solid #157ed2;
		cursor: pointer;
		border-radius: 2px;
		padding: 0 10px;
		margin: 0 5px 5px 0;
		color: #fff;
		background: #59b5ff;
		width: auto;
		font-size: 14px;
		height: 32px;
	}
	
	.el-table /deep/ .el-table__body-wrapper tbody tr td .edit:hover {
		opacity: 0.8;
	}
	
	.el-table /deep/ .el-table__body-wrapper tbody tr td .del {
		border: 0px solid #157ed2;
		cursor: pointer;
		border-radius: 2px;
		padding: 0 10px;
		margin: 0 5px 5px 0;
		color: #fff;
		background: #3bc1ff;
		width: auto;
		font-size: 14px;
		height: 32px;
	}
	
	.el-table /deep/ .el-table__body-wrapper tbody tr td .del:hover {
		opacity: 0.8;
	}
	
	.el-table /deep/ .el-table__body-wrapper tbody tr td .btn8 {
		border: 0px solid #157ed2;
		cursor: pointer;
		border-radius: 2px;
		padding: 0 10px;
		margin: 0 5px 5px 0;
		color: #fff;
		background: #55d8ec;
		width: auto;
		font-size: 14px;
		height: 32px;
	}
	
	.el-table /deep/ .el-table__body-wrapper tbody tr td .btn8:hover {
		opacity: 0.8;
	}
	
	// pagination
	.main-content .el-pagination /deep/ .el-pagination__total {
		margin: 0 10px 0 0;
		color: #666;
		font-weight: 400;
		display: inline-block;
		vertical-align: top;
		font-size: inherit;
		line-height: 48px;
		height: 48px;
	}
	
	.main-content .el-pagination /deep/ .btn-prev {
		border: none;
		padding: 0 5px 0 0;
		margin: 0;
		color: #5E5E5E;
		display: inline-block;
		vertical-align: top;
		font-size: 16px;
		border-color: #C2C2C2;
		line-height: auto;
		border-radius: 2px;
		left: 20px;
		background: none;
		border-width: 0;
		border-style: solid;
		min-width: 35px;
		height: 30px;
	}
	
	.main-content .el-pagination /deep/ .btn-next {
		border: none;
		padding: 0  0 0 5px;
		margin: 0;
		color: #5E5E5E;
		display: inline-block;
		vertical-align: top;
		font-size: 16px;
		border-color: #C2C2C2;
		line-height: auto;
		right: 0;
		border-radius: 2px;
		background: none;
		border-width: 0;
		border-style: solid;
		min-width: 35px;
		height: 50px;
	}
	
	.main-content .el-pagination /deep/ .btn-prev:disabled {
		border: none;
		padding: 0 5px 0 0;
		margin: 0;
		color: #5E5E5E;
		display: inline-block;
		vertical-align: top;
		font-size: 16px;
		border-color: #C2C2C2;
		line-height: auto;
		right: 0;
		border-radius: 2px;
		left: 20px;
		background: none;
		border-width: 0;
		border-style: solid;
		min-width: 35px;
		height: 30px;
	}
	
	.main-content .el-pagination /deep/ .btn-next:disabled {
		border: none;
		padding: 0 5px 0 0;
		margin: 0;
		color: #5E5E5E;
		display: inline-block;
		vertical-align: top;
		font-size: 16px;
		border-color: #C2C2C2;
		line-height: auto;
		right: 0;
		border-radius: 2px;
		left: 20px;
		background: none;
		border-width: 0;
		border-style: solid;
		min-width: 35px;
		height: 30px;
	}

	.main-content .el-pagination /deep/ .el-pager {
		padding: 0;
		margin: 0;
		display: flex;
		align-items: center;
	}

	.main-content .el-pagination /deep/ .el-pager .number {
		cursor: pointer;
		border-radius: 2px;
		padding: 0 10px;
		margin: 0 5px 0 0;
		color: #000;
		background: #fff;
		display: block;
		vertical-align: top;
		font-size: 14px;
		line-height: 30px;
		text-align: center;
		height: 30px;
	}
	
	.main-content .el-pagination /deep/ .el-pager .number:hover {
		cursor: default;
		padding: 0 10px;
		color: #fff;
		display: flex;
		vertical-align: top;
		font-size: 14px;
		line-height: 30px;
		border-radius: 2px;
		background: #348CB4;
		width: 28px;
		justify-content: center;
		text-align: center;
		height: 30px;
	}
	
	.main-content .el-pagination /deep/ .el-pager .number.active {
		cursor: default;
		padding: 0 10px;
		margin: 0 5px 0 0;
		color: #fff;
		display: flex;
		vertical-align: top;
		font-size: 14px;
		line-height: 30px;
		border-radius: 2px;
		background: #348CB4;
		width: 28px;
		justify-content: center;
		text-align: center;
		height: 30px;
	}
	
	.main-content .el-pagination /deep/ .el-pagination__sizes {
		display: inline-block;
		vertical-align: top;
		font-size: 16px;
		line-height: 48px;
		height: 48px;
	}
	
	.main-content .el-pagination /deep/ .el-pagination__sizes .el-input {
		margin: 0 5px;
		width: 100px;
		position: relative;
	}
	
	.main-content .el-pagination /deep/ .el-pagination__sizes .el-input .el-input__inner {
		border: 1px solid #DCDFE6;
		cursor: pointer;
		padding: 0 25px 0 8px;
		color: #606266;
		display: inline-block;
		font-size: 16px;
		line-height: 28px;
		border-radius: 3px;
		outline: 0;
		background: #FFF;
		width: 100%;
		text-align: center;
		height: 28px;
	}
	
	.main-content .el-pagination /deep/ .el-pagination__sizes .el-input span.el-input__suffix {
		top: 0;
		position: absolute;
		right: 0;
		height: 100%;
	}
	
	.main-content .el-pagination /deep/ .el-pagination__sizes .el-input .el-input__suffix .el-select__caret {
		cursor: pointer;
		color: #C0C4CC;
		width: 25px;
		font-size: 14px;
		line-height: 48px;
		text-align: center;
	}
	
	.main-content .el-pagination /deep/ .el-pagination__jump {
		margin: 0 0 0 24px;
		color: #606266;
		display: inline-block;
		vertical-align: top;
		font-size: 16px;
		line-height: 48px;
		height: 48px;
	}
	
	.main-content .el-pagination /deep/ .el-pagination__jump .el-input {
		border-radius: 3px;
		padding: 0 2px;
		margin: 0 2px;
		display: inline-block;
		width: 50px;
		font-size: 14px;
		line-height: 18px;
		position: relative;
		text-align: center;
		height: 28px;
	}
	
	.main-content .el-pagination /deep/ .el-pagination__jump .el-input .el-input__inner {
		border: 1px solid #DCDFE6;
		cursor: pointer;
		padding: 0 3px;
		color: #606266;
		display: inline-block;
		font-size: 16px;
		line-height: 28px;
		border-radius: 3px;
		outline: 0;
		background: #FFF;
		width: 100%;
		text-align: center;
		height: 28px;
	}
	
	// list one
	.one .list1-view {
		border: 0;
		cursor: pointer;
		border-radius: 0;
		padding: 0 15px;
		outline: none;
		margin: 5px 0;
		color: #fff;
		background: #EF8E6A;
		width: 45%;
		font-size: 16px;
		height: 29px;
	}
	
	.one .list1-view:hover {
		opacity: 0.8;
	}
	
	.one .list1-edit {
		border: 0;
		cursor: pointer;
		border-radius: 0;
		padding: 0 15px;
		outline: none;
		margin: 5px 0;
		color: #fff;
		background: #348CB4;
		width: 45%;
		font-size: 16px;
		float: left;
		height: 29px;
	}
	
	.one .list1-edit:hover {
		opacity: 0.8;
	}
	
	.one .list1-del {
		border: 0;
		cursor: pointer;
		border-radius: 0;
		padding: 0 15px;
		outline: none;
		margin: 5px 0;
		color: #fff;
		background: #63D3F9;
		width: 45%;
		font-size: 16px;
		float: left;
		height: 29px;
	}
	
	.one .list1-del:hover {
		opacity: 0.8;
	}
	
	.one .list1-btn8 {
		border: 0;
		cursor: pointer;
		border-radius: 4px;
		padding: 0 24px;
		margin: 0 5px 5px 0;
		outline: none;
		color: #fff;
		background: rgba(255, 128, 0, 1);
		display: none;
		width: auto;
		font-size: 14px;
		height: 32px;
	}
	
	.one .list1-btn8:hover {
		opacity: 0.8;
	}
	
	.main-content .el-table .el-switch {
		display: inline-flex;
		vertical-align: middle;
		line-height: 30px;
		position: relative;
		align-items: center;
		height: 30px;
	}
	.main-content .el-table .el-switch /deep/ .el-switch__label--left {
		cursor: pointer;
		margin: 0 10px 0 0;
		color: #333;
		font-weight: 500;
		display: inline-block;
		vertical-align: middle;
		font-size: 16px;
		transition: .2s;
		height: 30px;
	}
	.main-content .el-table .el-switch /deep/ .el-switch__label--right {
		cursor: pointer;
		margin: 0 0 0 10px;
		color: #333;
		font-weight: 500;
		display: inline-block;
		vertical-align: middle;
		font-size: 16px;
		transition: .2s;
		height: 30px;
	}
	.main-content .el-table .el-switch /deep/ .el-switch__core {
		border: 1px solid #75c0d6;
		cursor: pointer;
		border-radius: 15px;
		margin: 0;
		background: #75c0d6;
		display: inline-block;
		width: 42px;
		box-sizing: border-box;
		transition: border-color .3s,background-color .3s;
		height: 20px;
	}
	.main-content .el-table .el-switch /deep/ .el-switch__core::after {
		border-radius: 100%;
		top: 1px;
		left: 1px;
		background: #fff;
		width: 16px;
		position: absolute;
		transition: all .3s;
		height: 16px;
	}
	.main-content .el-table .el-switch.is-checked /deep/ .el-switch__core::after {
		margin: 0 0 0 -18px;
		left: 100%;
	}
	
	.main-content .el-table .el-rate /deep/ .el-rate__item {
		cursor: pointer;
		display: inline-block;
		vertical-align: middle;
		font-size: 0;
		position: relative;
	}
	.main-content .el-table .el-rate /deep/ .el-rate__item .el-rate__icon {
		margin: 0 3px;
		display: inline-block;
		font-size: 18px;
		position: relative;
		transition: .3s;
	}

</style>
