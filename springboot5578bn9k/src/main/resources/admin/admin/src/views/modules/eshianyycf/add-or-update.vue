<template>
	<div class="addEdit-block">
		<el-form
			class="add-update-preview"
			ref="ruleForm"
			:model="ruleForm"
			:rules="rules"
			label-width="180px"
		>
			<template >
				<el-form-item class="input" v-if="type!='info'"  label="中文名" prop="cname" >
					<el-input v-model="ruleForm.cname" placeholder="中文名" clearable  :readonly="ro.cname"></el-input>
				</el-form-item>
				<el-form-item v-else class="input" label="中文名" prop="cname" >
					<el-input v-model="ruleForm.cname" placeholder="中文名" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="英文名" prop="ename" >
					<el-input v-model="ruleForm.ename" placeholder="英文名" clearable  :readonly="ro.ename"></el-input>
				</el-form-item>
				<el-form-item v-else class="input" label="英文名" prop="ename" >
					<el-input v-model="ruleForm.ename" placeholder="英文名" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="食品分类" prop="spfenlei" >
					<el-input v-model="ruleForm.spfenlei" placeholder="食品分类" clearable  :readonly="ro.spfenlei"></el-input>
				</el-form-item>
				<el-form-item v-else class="input" label="食品分类" prop="spfenlei" >
					<el-input v-model="ruleForm.spfenlei" placeholder="食品分类" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="可食部%" prop="keshibu" >
					<el-input-number v-model="ruleForm.keshibu" placeholder="可食部%" :disabled="ro.keshibu"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="可食部%" prop="keshibu" >
					<el-input v-model="ruleForm.keshibu" placeholder="可食部%" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="来源" prop="laiyuan" >
					<el-input v-model="ruleForm.laiyuan" placeholder="来源" clearable  :readonly="ro.laiyuan"></el-input>
				</el-form-item>
				<el-form-item v-else class="input" label="来源" prop="laiyuan" >
					<el-input v-model="ruleForm.laiyuan" placeholder="来源" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="产地" prop="chandi" >
					<el-input v-model="ruleForm.chandi" placeholder="产地" clearable  :readonly="ro.chandi"></el-input>
				</el-form-item>
				<el-form-item v-else class="input" label="产地" prop="chandi" >
					<el-input v-model="ruleForm.chandi" placeholder="产地" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="能量(千焦)" prop="nengliang" >
					<el-input-number v-model="ruleForm.nengliang" placeholder="能量(千焦)" :disabled="ro.nengliang"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="能量(千焦)" prop="nengliang" >
					<el-input v-model="ruleForm.nengliang" placeholder="能量(千焦)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="蛋白质(克)" prop="danbaizhi" >
					<el-input-number v-model="ruleForm.danbaizhi" placeholder="蛋白质(克)" :disabled="ro.danbaizhi"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="蛋白质(克)" prop="danbaizhi" >
					<el-input v-model="ruleForm.danbaizhi" placeholder="蛋白质(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="脂肪(克)" prop="zhifang" >
					<el-input-number v-model="ruleForm.zhifang" placeholder="脂肪(克)" :disabled="ro.zhifang"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="脂肪(克)" prop="zhifang" >
					<el-input v-model="ruleForm.zhifang" placeholder="脂肪(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="碳水化合物(克)" prop="tshhw" >
					<el-input-number v-model="ruleForm.tshhw" placeholder="碳水化合物(克)" :disabled="ro.tshhw"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="碳水化合物(克)" prop="tshhw" >
					<el-input v-model="ruleForm.tshhw" placeholder="碳水化合物(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="胆固醇(毫克)" prop="dangc" >
					<el-input-number v-model="ruleForm.dangc" placeholder="胆固醇(毫克)" :disabled="ro.dangc"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="胆固醇(毫克)" prop="dangc" >
					<el-input v-model="ruleForm.dangc" placeholder="胆固醇(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="饱和脂肪酸(克)" prop="baohezhifang" >
					<el-input-number v-model="ruleForm.baohezhifang" placeholder="饱和脂肪酸(克)" :disabled="ro.baohezhifang"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="饱和脂肪酸(克)" prop="baohezhifang" >
					<el-input v-model="ruleForm.baohezhifang" placeholder="饱和脂肪酸(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="反式脂肪酸(克)" prop="fanshizfs" >
					<el-input-number v-model="ruleForm.fanshizfs" placeholder="反式脂肪酸(克)" :disabled="ro.fanshizfs"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="反式脂肪酸(克)" prop="fanshizfs" >
					<el-input v-model="ruleForm.fanshizfs" placeholder="反式脂肪酸(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="单不饱和脂肪酸(克)" prop="dbbhzfs" >
					<el-input-number v-model="ruleForm.dbbhzfs" placeholder="单不饱和脂肪酸(克)" :disabled="ro.dbbhzfs"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="单不饱和脂肪酸(克)" prop="dbbhzfs" >
					<el-input v-model="ruleForm.dbbhzfs" placeholder="单不饱和脂肪酸(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="多不饱和脂肪酸(克)" prop="duobbhzfs" >
					<el-input-number v-model="ruleForm.duobbhzfs" placeholder="多不饱和脂肪酸(克)" :disabled="ro.duobbhzfs"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="多不饱和脂肪酸(克)" prop="duobbhzfs" >
					<el-input v-model="ruleForm.duobbhzfs" placeholder="多不饱和脂肪酸(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="糖(克)" prop="tang" >
					<el-input-number v-model="ruleForm.tang" placeholder="糖(克)" :disabled="ro.tang"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="糖(克)" prop="tang" >
					<el-input v-model="ruleForm.tang" placeholder="糖(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="乳糖(克)" prop="rutang" >
					<el-input-number v-model="ruleForm.rutang" placeholder="乳糖(克)" :disabled="ro.rutang"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="乳糖(克)" prop="rutang" >
					<el-input v-model="ruleForm.rutang" placeholder="乳糖(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="膳食纤维(克)" prop="sanshiqw" >
					<el-input-number v-model="ruleForm.sanshiqw" placeholder="膳食纤维(克)" :disabled="ro.sanshiqw"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="膳食纤维(克)" prop="sanshiqw" >
					<el-input v-model="ruleForm.sanshiqw" placeholder="膳食纤维(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="可溶性膳食纤维(克)" prop="kesxssqw" >
					<el-input-number v-model="ruleForm.kesxssqw" placeholder="可溶性膳食纤维(克)" :disabled="ro.kesxssqw"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="可溶性膳食纤维(克)" prop="kesxssqw" >
					<el-input v-model="ruleForm.kesxssqw" placeholder="可溶性膳食纤维(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="不溶性膳食纤维(克)" prop="bsxssqw" >
					<el-input-number v-model="ruleForm.bsxssqw" placeholder="不溶性膳食纤维(克)" :disabled="ro.bsxssqw"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="不溶性膳食纤维(克)" prop="bsxssqw" >
					<el-input v-model="ruleForm.bsxssqw" placeholder="不溶性膳食纤维(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="钠(毫克)" prop="jinshuna" >
					<el-input-number v-model="ruleForm.jinshuna" placeholder="钠(毫克)" :disabled="ro.jinshuna"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="钠(毫克)" prop="jinshuna" >
					<el-input v-model="ruleForm.jinshuna" placeholder="钠(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="维生素A(微克视黄醇当量)" prop="weishengshua" >
					<el-input-number v-model="ruleForm.weishengshua" placeholder="维生素A(微克视黄醇当量)" :disabled="ro.weishengshua"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="维生素A(微克视黄醇当量)" prop="weishengshua" >
					<el-input v-model="ruleForm.weishengshua" placeholder="维生素A(微克视黄醇当量)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="维生素D(微克)" prop="weishengshud" >
					<el-input-number v-model="ruleForm.weishengshud" placeholder="维生素D(微克)" :disabled="ro.weishengshud"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="维生素D(微克)" prop="weishengshud" >
					<el-input v-model="ruleForm.weishengshud" placeholder="维生素D(微克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="维生素E(毫克α-生育酚当量)" prop="weishengshue" >
					<el-input-number v-model="ruleForm.weishengshue" placeholder="维生素E(毫克α-生育酚当量)" :disabled="ro.weishengshue"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="维生素E(毫克α-生育酚当量)" prop="weishengshue" >
					<el-input v-model="ruleForm.weishengshue" placeholder="维生素E(毫克α-生育酚当量)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="维生素K(微克)" prop="weishengshuk" >
					<el-input-number v-model="ruleForm.weishengshuk" placeholder="维生素K(微克)" :disabled="ro.weishengshuk"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="维生素K(微克)" prop="weishengshuk" >
					<el-input v-model="ruleForm.weishengshuk" placeholder="维生素K(微克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="维生素B1（硫胺素）(毫克)" prop="weishengshub1" >
					<el-input-number v-model="ruleForm.weishengshub1" placeholder="维生素B1（硫胺素）(毫克)" :disabled="ro.weishengshub1"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="维生素B1（硫胺素）(毫克)" prop="weishengshub1" >
					<el-input v-model="ruleForm.weishengshub1" placeholder="维生素B1（硫胺素）(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="维生素B2（核黄素）(毫克)" prop="weishengshub2" >
					<el-input-number v-model="ruleForm.weishengshub2" placeholder="维生素B2（核黄素）(毫克)" :disabled="ro.weishengshub2"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="维生素B2（核黄素）(毫克)" prop="weishengshub2" >
					<el-input v-model="ruleForm.weishengshub2" placeholder="维生素B2（核黄素）(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="维生素B6(毫克)" prop="weishengshub6" >
					<el-input-number v-model="ruleForm.weishengshub6" placeholder="维生素B6(毫克)" :disabled="ro.weishengshub6"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="维生素B6(毫克)" prop="weishengshub6" >
					<el-input v-model="ruleForm.weishengshub6" placeholder="维生素B6(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="维生素B12(微克)" prop="weishengshub12" >
					<el-input-number v-model="ruleForm.weishengshub12" placeholder="维生素B12(微克)" :disabled="ro.weishengshub12"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="维生素B12(微克)" prop="weishengshub12" >
					<el-input v-model="ruleForm.weishengshub12" placeholder="维生素B12(微克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="维生素C（抗坏血酸）(毫克)" prop="weishengshuc" >
					<el-input-number v-model="ruleForm.weishengshuc" placeholder="维生素C（抗坏血酸）(毫克)" :disabled="ro.weishengshuc"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="维生素C（抗坏血酸）(毫克)" prop="weishengshuc" >
					<el-input v-model="ruleForm.weishengshuc" placeholder="维生素C（抗坏血酸）(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="烟酸（烟酰胺）(毫克)" prop="yanshuan" >
					<el-input-number v-model="ruleForm.yanshuan" placeholder="烟酸（烟酰胺）(毫克)" :disabled="ro.yanshuan"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="烟酸（烟酰胺）(毫克)" prop="yanshuan" >
					<el-input v-model="ruleForm.yanshuan" placeholder="烟酸（烟酰胺）(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="叶酸(微克叶酸当量)" prop="yeshuan" >
					<el-input-number v-model="ruleForm.yeshuan" placeholder="叶酸(微克叶酸当量)" :disabled="ro.yeshuan"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="叶酸(微克叶酸当量)" prop="yeshuan" >
					<el-input v-model="ruleForm.yeshuan" placeholder="叶酸(微克叶酸当量)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="泛酸(毫克)" prop="fanshuan" >
					<el-input-number v-model="ruleForm.fanshuan" placeholder="泛酸(毫克)" :disabled="ro.fanshuan"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="泛酸(毫克)" prop="fanshuan" >
					<el-input v-model="ruleForm.fanshuan" placeholder="泛酸(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="生物素(微克)" prop="shenwushu" >
					<el-input-number v-model="ruleForm.shenwushu" placeholder="生物素(微克)" :disabled="ro.shenwushu"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="生物素(微克)" prop="shenwushu" >
					<el-input v-model="ruleForm.shenwushu" placeholder="生物素(微克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="胆碱(毫克)" prop="danjian" >
					<el-input-number v-model="ruleForm.danjian" placeholder="胆碱(毫克)" :disabled="ro.danjian"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="胆碱(毫克)" prop="danjian" >
					<el-input v-model="ruleForm.danjian" placeholder="胆碱(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="磷(毫克)" prop="jinshulin" >
					<el-input-number v-model="ruleForm.jinshulin" placeholder="磷(毫克)" :disabled="ro.jinshulin"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="磷(毫克)" prop="jinshulin" >
					<el-input v-model="ruleForm.jinshulin" placeholder="磷(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="钾(毫克)" prop="jinshujia" >
					<el-input-number v-model="ruleForm.jinshujia" placeholder="钾(毫克)" :disabled="ro.jinshujia"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="钾(毫克)" prop="jinshujia" >
					<el-input v-model="ruleForm.jinshujia" placeholder="钾(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="镁(毫克)" prop="jinshumei" >
					<el-input-number v-model="ruleForm.jinshumei" placeholder="镁(毫克)" :disabled="ro.jinshumei"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="镁(毫克)" prop="jinshumei" >
					<el-input v-model="ruleForm.jinshumei" placeholder="镁(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="钙(毫克)" prop="jinshugai" >
					<el-input-number v-model="ruleForm.jinshugai" placeholder="钙(毫克)" :disabled="ro.jinshugai"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="钙(毫克)" prop="jinshugai" >
					<el-input v-model="ruleForm.jinshugai" placeholder="钙(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="铁(毫克)" prop="jinshutie" >
					<el-input-number v-model="ruleForm.jinshutie" placeholder="铁(毫克)" :disabled="ro.jinshutie"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="铁(毫克)" prop="jinshutie" >
					<el-input v-model="ruleForm.jinshutie" placeholder="铁(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="锌(毫克)" prop="jinshuxin" >
					<el-input-number v-model="ruleForm.jinshuxin" placeholder="锌(毫克)" :disabled="ro.jinshuxin"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="锌(毫克)" prop="jinshuxin" >
					<el-input v-model="ruleForm.jinshuxin" placeholder="锌(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="碘(微克)" prop="jinshudian" >
					<el-input-number v-model="ruleForm.jinshudian" placeholder="碘(微克)" :disabled="ro.jinshudian"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="碘(微克)" prop="jinshudian" >
					<el-input v-model="ruleForm.jinshudian" placeholder="碘(微克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="硒(微克)" prop="jinshudxi" >
					<el-input-number v-model="ruleForm.jinshudxi" placeholder="硒(微克)" :disabled="ro.jinshudxi"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="硒(微克)" prop="jinshudxi" >
					<el-input v-model="ruleForm.jinshudxi" placeholder="硒(微克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="铜(毫克)" prop="jinshutong" >
					<el-input-number v-model="ruleForm.jinshutong" placeholder="铜(毫克)" :disabled="ro.jinshutong"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="铜(毫克)" prop="jinshutong" >
					<el-input v-model="ruleForm.jinshutong" placeholder="铜(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="氟(毫克)" prop="jinshufu" >
					<el-input-number v-model="ruleForm.jinshufu" placeholder="氟(毫克)" :disabled="ro.jinshufu"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="氟(毫克)" prop="jinshufu" >
					<el-input v-model="ruleForm.jinshufu" placeholder="氟(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="锰(毫克)" prop="jinshumeng" >
					<el-input-number v-model="ruleForm.jinshumeng" placeholder="锰(毫克)" :disabled="ro.jinshumeng"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="锰(毫克)" prop="jinshumeng" >
					<el-input v-model="ruleForm.jinshumeng" placeholder="锰(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="δ-E(毫克)" prop="deltae" >
					<el-input-number v-model="ruleForm.deltae" placeholder="δ-E(毫克)" :disabled="ro.deltae"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="δ-E(毫克)" prop="deltae" >
					<el-input v-model="ruleForm.deltae" placeholder="δ-E(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="(β-γ)-E(毫克)" prop="beitae" >
					<el-input-number v-model="ruleForm.beitae" placeholder="(β-γ)-E(毫克)" :disabled="ro.beitae"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="(β-γ)-E(毫克)" prop="beitae" >
					<el-input v-model="ruleForm.beitae" placeholder="(β-γ)-E(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="α-E(毫克)" prop="aerfae" >
					<el-input-number v-model="ruleForm.aerfae" placeholder="α-E(毫克)" :disabled="ro.aerfae"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="α-E(毫克)" prop="aerfae" >
					<el-input v-model="ruleForm.aerfae" placeholder="α-E(毫克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="胡萝卜素(微克)" prop="hulubo" >
					<el-input-number v-model="ruleForm.hulubo" placeholder="胡萝卜素(微克)" :disabled="ro.hulubo"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="胡萝卜素(微克)" prop="hulubo" >
					<el-input v-model="ruleForm.hulubo" placeholder="胡萝卜素(微克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="脂肪酸（总）(克)" prop="zhifansz" >
					<el-input-number v-model="ruleForm.zhifansz" placeholder="脂肪酸（总）(克)" :disabled="ro.zhifansz"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="脂肪酸（总）(克)" prop="zhifansz" >
					<el-input v-model="ruleForm.zhifansz" placeholder="脂肪酸（总）(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="灰分(克)" prop="huifen" >
					<el-input-number v-model="ruleForm.huifen" placeholder="灰分(克)" :disabled="ro.huifen"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="灰分(克)" prop="huifen" >
					<el-input v-model="ruleForm.huifen" placeholder="灰分(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="水分(克)" prop="shuifen" >
					<el-input-number v-model="ruleForm.shuifen" placeholder="水分(克)" :disabled="ro.shuifen"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="水分(克)" prop="shuifen" >
					<el-input v-model="ruleForm.shuifen" placeholder="水分(克)" readonly></el-input>
				</el-form-item>
				<el-form-item class="input" v-if="type!='info'"  label="能量(千卡)" prop="nengliangqk" >
					<el-input-number v-model="ruleForm.nengliangqk" placeholder="能量(千卡)" :disabled="ro.nengliangqk"></el-input-number>
				</el-form-item>
				<el-form-item v-else class="input" label="能量(千卡)" prop="nengliangqk" >
					<el-input v-model="ruleForm.nengliangqk" placeholder="能量(千卡)" readonly></el-input>
				</el-form-item>
			</template>
			<el-form-item class="textarea" v-if="type!='info'" label="详情链接" prop="xqurl" >
				<el-input
					style="min-width: 200px; max-width: 600px;"
					type="textarea"
					:rows="8"
					placeholder="详情链接"
					v-model="ruleForm.xqurl" >
				</el-input>
			</el-form-item>
			<el-form-item v-else-if="ruleForm.xqurl" label="详情链接" prop="xqurl" >
				<span class="text">{{ruleForm.xqurl}}</span>
			</el-form-item>
			<el-form-item class="btn">
				<el-button class="btn3"  v-if="type!='info'" type="success" @click="onSubmit">
					<span class="icon iconfont icon-xihuan"></span>
					提交
				</el-button>
				<el-button class="btn4" v-if="type!='info'" type="success" @click="back()">
					<span class="icon iconfont icon-xihuan"></span>
					取消
				</el-button>
				<el-button class="btn5" v-if="type=='info'" type="success" @click="back()">
					<span class="icon iconfont icon-xihuan"></span>
					返回
				</el-button>
			</el-form-item>
		</el-form>
    

	</div>
</template>
<script>
	import { 
		isNumber,
		isIntNumer,
		isURL,
	} from "@/utils/validate";
	export default {
		data() {
			var validateUrl = (rule, value, callback) => {
				if(!value){
					callback();
				} else if (!isURL(value)) {
					callback(new Error("请输入正确的URL地址"));
				} else {
					callback();
				}
			};
			var validateNumber = (rule, value, callback) => {
				if(!value){
					callback();
				} else if (!isNumber(value)) {
					callback(new Error("请输入数字"));
				} else {
					callback();
				}
			};
			var validateIntNumber = (rule, value, callback) => {
				if(!value){
					callback();
				} else if (!isIntNumer(value)) {
					callback(new Error("请输入整数"));
				} else {
					callback();
				}
			};
			return {
				id: '',
				type: '',
			
			
				ro:{
					cname : false,
					ename : false,
					spfenlei : false,
					keshibu : false,
					laiyuan : false,
					chandi : false,
					nengliang : false,
					danbaizhi : false,
					zhifang : false,
					tshhw : false,
					dangc : false,
					baohezhifang : false,
					fanshizfs : false,
					dbbhzfs : false,
					duobbhzfs : false,
					tang : false,
					rutang : false,
					sanshiqw : false,
					kesxssqw : false,
					bsxssqw : false,
					jinshuna : false,
					weishengshua : false,
					weishengshud : false,
					weishengshue : false,
					weishengshuk : false,
					weishengshub1 : false,
					weishengshub2 : false,
					weishengshub6 : false,
					weishengshub12 : false,
					weishengshuc : false,
					yanshuan : false,
					yeshuan : false,
					fanshuan : false,
					shenwushu : false,
					danjian : false,
					jinshulin : false,
					jinshujia : false,
					jinshumei : false,
					jinshugai : false,
					jinshutie : false,
					jinshuxin : false,
					jinshudian : false,
					jinshudxi : false,
					jinshutong : false,
					jinshufu : false,
					jinshumeng : false,
					deltae : false,
					beitae : false,
					aerfae : false,
					hulubo : false,
					zhifansz : false,
					huifen : false,
					shuifen : false,
					nengliangqk : false,
					xqurl : false,
					storeupnum : false,
				},
			
				ruleForm: {
					cname: '',
					ename: '',
					spfenlei: '',
					keshibu: '',
					laiyuan: '',
					chandi: '',
					nengliang: '',
					danbaizhi: '',
					zhifang: '',
					tshhw: '',
					dangc: '',
					baohezhifang: '',
					fanshizfs: '',
					dbbhzfs: '',
					duobbhzfs: '',
					tang: '',
					rutang: '',
					sanshiqw: '',
					kesxssqw: '',
					bsxssqw: '',
					jinshuna: '',
					weishengshua: '',
					weishengshud: '',
					weishengshue: '',
					weishengshuk: '',
					weishengshub1: '',
					weishengshub2: '',
					weishengshub6: '',
					weishengshub12: '',
					weishengshuc: '',
					yanshuan: '',
					yeshuan: '',
					fanshuan: '',
					shenwushu: '',
					danjian: '',
					jinshulin: '',
					jinshujia: '',
					jinshumei: '',
					jinshugai: '',
					jinshutie: '',
					jinshuxin: '',
					jinshudian: '',
					jinshudxi: '',
					jinshutong: '',
					jinshufu: '',
					jinshumeng: '',
					deltae: '',
					beitae: '',
					aerfae: '',
					hulubo: '',
					zhifansz: '',
					huifen: '',
					shuifen: '',
					nengliangqk: '',
					xqurl: '',
				},

				rules: {
					cname: [
					],
					ename: [
					],
					spfenlei: [
					],
					keshibu: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					laiyuan: [
					],
					chandi: [
					],
					nengliang: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					danbaizhi: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					zhifang: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					tshhw: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					dangc: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					baohezhifang: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					fanshizfs: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					dbbhzfs: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					duobbhzfs: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					tang: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					rutang: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					sanshiqw: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					kesxssqw: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					bsxssqw: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					jinshuna: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					weishengshua: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					weishengshud: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					weishengshue: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					weishengshuk: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					weishengshub1: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					weishengshub2: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					weishengshub6: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					weishengshub12: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					weishengshuc: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					yanshuan: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					yeshuan: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					fanshuan: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					shenwushu: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					danjian: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					jinshulin: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					jinshujia: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					jinshumei: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					jinshugai: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					jinshutie: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					jinshuxin: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					jinshudian: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					jinshudxi: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					jinshutong: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					jinshufu: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					jinshumeng: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					deltae: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					beitae: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					aerfae: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					hulubo: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					zhifansz: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					huifen: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					shuifen: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					nengliangqk: [
						{ validator: validateNumber, trigger: 'blur' },
					],
					xqurl: [
						{ validator: validateUrl, trigger: 'blur' },
					],
					storeupnum: [
						{ validator: validateIntNumber, trigger: 'blur' },
					],
				},
			};
		},
		props: ["parent"],
		computed: {



		},
		components: {
		},
		created() {
		},
		methods: {
			// 下载
			download(file){
				window.open(`${file}`)
			},
			// 初始化
			init(id,type) {
				if (id) {
					this.id = id;
					this.type = type;
				}
				if(this.type=='info'||this.type=='else'||this.type=='msg'){
					this.info(id);
				}else if(this.type=='logistics'){
					for(let x in this.ro) {
						this.ro[x] = true
					}
					this.logistics=false;
					this.info(id);
				}else if(this.type=='cross'){
					var obj = this.$storage.getObj('crossObj');
					for (var o in obj){
						if(o=='cname'){
							this.ruleForm.cname = obj[o];
							this.ro.cname = true;
							continue;
						}
						if(o=='ename'){
							this.ruleForm.ename = obj[o];
							this.ro.ename = true;
							continue;
						}
						if(o=='spfenlei'){
							this.ruleForm.spfenlei = obj[o];
							this.ro.spfenlei = true;
							continue;
						}
						if(o=='keshibu'){
							this.ruleForm.keshibu = obj[o];
							this.ro.keshibu = true;
							continue;
						}
						if(o=='laiyuan'){
							this.ruleForm.laiyuan = obj[o];
							this.ro.laiyuan = true;
							continue;
						}
						if(o=='chandi'){
							this.ruleForm.chandi = obj[o];
							this.ro.chandi = true;
							continue;
						}
						if(o=='nengliang'){
							this.ruleForm.nengliang = obj[o];
							this.ro.nengliang = true;
							continue;
						}
						if(o=='danbaizhi'){
							this.ruleForm.danbaizhi = obj[o];
							this.ro.danbaizhi = true;
							continue;
						}
						if(o=='zhifang'){
							this.ruleForm.zhifang = obj[o];
							this.ro.zhifang = true;
							continue;
						}
						if(o=='tshhw'){
							this.ruleForm.tshhw = obj[o];
							this.ro.tshhw = true;
							continue;
						}
						if(o=='dangc'){
							this.ruleForm.dangc = obj[o];
							this.ro.dangc = true;
							continue;
						}
						if(o=='baohezhifang'){
							this.ruleForm.baohezhifang = obj[o];
							this.ro.baohezhifang = true;
							continue;
						}
						if(o=='fanshizfs'){
							this.ruleForm.fanshizfs = obj[o];
							this.ro.fanshizfs = true;
							continue;
						}
						if(o=='dbbhzfs'){
							this.ruleForm.dbbhzfs = obj[o];
							this.ro.dbbhzfs = true;
							continue;
						}
						if(o=='duobbhzfs'){
							this.ruleForm.duobbhzfs = obj[o];
							this.ro.duobbhzfs = true;
							continue;
						}
						if(o=='tang'){
							this.ruleForm.tang = obj[o];
							this.ro.tang = true;
							continue;
						}
						if(o=='rutang'){
							this.ruleForm.rutang = obj[o];
							this.ro.rutang = true;
							continue;
						}
						if(o=='sanshiqw'){
							this.ruleForm.sanshiqw = obj[o];
							this.ro.sanshiqw = true;
							continue;
						}
						if(o=='kesxssqw'){
							this.ruleForm.kesxssqw = obj[o];
							this.ro.kesxssqw = true;
							continue;
						}
						if(o=='bsxssqw'){
							this.ruleForm.bsxssqw = obj[o];
							this.ro.bsxssqw = true;
							continue;
						}
						if(o=='jinshuna'){
							this.ruleForm.jinshuna = obj[o];
							this.ro.jinshuna = true;
							continue;
						}
						if(o=='weishengshua'){
							this.ruleForm.weishengshua = obj[o];
							this.ro.weishengshua = true;
							continue;
						}
						if(o=='weishengshud'){
							this.ruleForm.weishengshud = obj[o];
							this.ro.weishengshud = true;
							continue;
						}
						if(o=='weishengshue'){
							this.ruleForm.weishengshue = obj[o];
							this.ro.weishengshue = true;
							continue;
						}
						if(o=='weishengshuk'){
							this.ruleForm.weishengshuk = obj[o];
							this.ro.weishengshuk = true;
							continue;
						}
						if(o=='weishengshub1'){
							this.ruleForm.weishengshub1 = obj[o];
							this.ro.weishengshub1 = true;
							continue;
						}
						if(o=='weishengshub2'){
							this.ruleForm.weishengshub2 = obj[o];
							this.ro.weishengshub2 = true;
							continue;
						}
						if(o=='weishengshub6'){
							this.ruleForm.weishengshub6 = obj[o];
							this.ro.weishengshub6 = true;
							continue;
						}
						if(o=='weishengshub12'){
							this.ruleForm.weishengshub12 = obj[o];
							this.ro.weishengshub12 = true;
							continue;
						}
						if(o=='weishengshuc'){
							this.ruleForm.weishengshuc = obj[o];
							this.ro.weishengshuc = true;
							continue;
						}
						if(o=='yanshuan'){
							this.ruleForm.yanshuan = obj[o];
							this.ro.yanshuan = true;
							continue;
						}
						if(o=='yeshuan'){
							this.ruleForm.yeshuan = obj[o];
							this.ro.yeshuan = true;
							continue;
						}
						if(o=='fanshuan'){
							this.ruleForm.fanshuan = obj[o];
							this.ro.fanshuan = true;
							continue;
						}
						if(o=='shenwushu'){
							this.ruleForm.shenwushu = obj[o];
							this.ro.shenwushu = true;
							continue;
						}
						if(o=='danjian'){
							this.ruleForm.danjian = obj[o];
							this.ro.danjian = true;
							continue;
						}
						if(o=='jinshulin'){
							this.ruleForm.jinshulin = obj[o];
							this.ro.jinshulin = true;
							continue;
						}
						if(o=='jinshujia'){
							this.ruleForm.jinshujia = obj[o];
							this.ro.jinshujia = true;
							continue;
						}
						if(o=='jinshumei'){
							this.ruleForm.jinshumei = obj[o];
							this.ro.jinshumei = true;
							continue;
						}
						if(o=='jinshugai'){
							this.ruleForm.jinshugai = obj[o];
							this.ro.jinshugai = true;
							continue;
						}
						if(o=='jinshutie'){
							this.ruleForm.jinshutie = obj[o];
							this.ro.jinshutie = true;
							continue;
						}
						if(o=='jinshuxin'){
							this.ruleForm.jinshuxin = obj[o];
							this.ro.jinshuxin = true;
							continue;
						}
						if(o=='jinshudian'){
							this.ruleForm.jinshudian = obj[o];
							this.ro.jinshudian = true;
							continue;
						}
						if(o=='jinshudxi'){
							this.ruleForm.jinshudxi = obj[o];
							this.ro.jinshudxi = true;
							continue;
						}
						if(o=='jinshutong'){
							this.ruleForm.jinshutong = obj[o];
							this.ro.jinshutong = true;
							continue;
						}
						if(o=='jinshufu'){
							this.ruleForm.jinshufu = obj[o];
							this.ro.jinshufu = true;
							continue;
						}
						if(o=='jinshumeng'){
							this.ruleForm.jinshumeng = obj[o];
							this.ro.jinshumeng = true;
							continue;
						}
						if(o=='deltae'){
							this.ruleForm.deltae = obj[o];
							this.ro.deltae = true;
							continue;
						}
						if(o=='beitae'){
							this.ruleForm.beitae = obj[o];
							this.ro.beitae = true;
							continue;
						}
						if(o=='aerfae'){
							this.ruleForm.aerfae = obj[o];
							this.ro.aerfae = true;
							continue;
						}
						if(o=='hulubo'){
							this.ruleForm.hulubo = obj[o];
							this.ro.hulubo = true;
							continue;
						}
						if(o=='zhifansz'){
							this.ruleForm.zhifansz = obj[o];
							this.ro.zhifansz = true;
							continue;
						}
						if(o=='huifen'){
							this.ruleForm.huifen = obj[o];
							this.ro.huifen = true;
							continue;
						}
						if(o=='shuifen'){
							this.ruleForm.shuifen = obj[o];
							this.ro.shuifen = true;
							continue;
						}
						if(o=='nengliangqk'){
							this.ruleForm.nengliangqk = obj[o];
							this.ro.nengliangqk = true;
							continue;
						}
						if(o=='xqurl'){
							this.ruleForm.xqurl = obj[o];
							this.ro.xqurl = true;
							continue;
						}
						if(o=='storeupnum'){
							this.ruleForm.storeupnum = obj[o];
							this.ro.storeupnum = true;
							continue;
						}
					}
				}
			
			},
			// 多级联动参数

			info(id) {
				this.$http({
					url: `eshianyycf/info/${id}`,
					method: "get"
				}).then(({ data }) => {
					if (data && data.code === 0) {
						this.ruleForm = data.data;
						//解决前台上传图片后台不显示的问题
						let reg=new RegExp('../../../upload','g')//g代表全部
					} else {
						this.$message.error(data.msg);
					}
				});
			},

			// 提交
			async onSubmit() {
					var objcross = this.$storage.getObj('crossObj');
					if(!this.ruleForm.id) {
						delete this.ruleForm.userid
					}
					await this.$refs["ruleForm"].validate(async valid => {
						if (valid) {
							if(this.type=='cross'){
								var statusColumnName = this.$storage.get('statusColumnName');
								var statusColumnValue = this.$storage.get('statusColumnValue');
								if(statusColumnName!='') {
									var obj = this.$storage.getObj('crossObj');
									if(statusColumnName && !statusColumnName.startsWith("[")) {
										for (var o in obj){
											if(o==statusColumnName){
												obj[o] = statusColumnValue;
											}
										}
										var table = this.$storage.get('crossTable');
										await this.$http({
											url: `${table}/update`,
											method: "post",
											data: obj
										}).then(({ data }) => {});
									}
								}
							}
							
							await this.$http({
								url: `eshianyycf/${!this.ruleForm.id ? "save" : "update"}`,
								method: "post",
								data: this.ruleForm
							}).then(async ({ data }) => {
								if (data && data.code === 0) {
									this.$message({
										message: "操作成功",
										type: "success",
										duration: 1500,
										onClose: () => {
											this.parent.showFlag = true;
											this.parent.addOrUpdateFlag = false;
											this.parent.eshianyycfCrossAddOrUpdateFlag = false;
											this.parent.search();
											this.parent.contentStyleChange();
										}
									});
								} else {
									this.$message.error(data.msg);
								}
							});
						}
					});
			},
			// 获取uuid
			getUUID () {
				return new Date().getTime();
			},
			// 返回
			back() {
				this.parent.showFlag = true;
				this.parent.addOrUpdateFlag = false;
				this.parent.eshianyycfCrossAddOrUpdateFlag = false;
				this.parent.contentStyleChange();
			},
		}
	};
</script>
<style lang="scss" scoped>
	.addEdit-block {
		padding: 78px 10px;
		background: #E2E2E2;
	}
	.add-update-preview {
		padding: 30px 30px 111px 30px;
		flex-direction: column;
		background: #fff;
		display: flex;
		border-color: #eee;
		border-width: 0px 0 0;
		border-style: solid;
	}
	.amap-wrapper {
		width: 100%;
		height: 500px;
	}
	
	.search-box {
		position: absolute;
	}
	
	.el-date-editor.el-input {
		width: auto;
	}
	.add-update-preview /deep/ .el-form-item {
		border: 0px solid #eee;
		padding: 0;
		margin: 0 0 26px 0;
		display: inline-block;
		width: 50%;
	}
	.add-update-preview .el-form-item /deep/ .el-form-item__label {
		padding: 0 10px 0 0;
		color: #000000;
		font-weight: 400;
		width: 180px;
		font-size: 16px;
		line-height: 40px;
		text-align: right;
	}
	
	.add-update-preview .el-form-item /deep/ .el-form-item__content {
		margin-left: 180px;
	}
	.add-update-preview .el-form-item span.text {
		border: 2px solid #000000;
		cursor: pointer;
		padding: 6px 15px;
		margin: 0 20px 0 0;
		color: #666;
		display: block;
		font-size: 15px;
		line-height: 24px;
		border-radius: 0px;
		word-break: break-all;
		background: #F4F4F4;
		width: 100%;
		text-align: left;
		height: auto;
	}
	
	.add-update-preview .el-input {
		width: 100%;
	}
	.add-update-preview .el-input /deep/ .el-input__inner {
		border: 2px solid #000000;
		border-radius: 5px  5px  5px  5px;
		padding: 0 12px;
		color: #666;
		background: #F4F4F4;
		width: 100%;
		font-size: 16px;
		min-width: 50%;
		height: 40px;
	}
	.add-update-preview .el-input /deep/ .el-input__inner[readonly="readonly"] {
		border: 2px solid #000000;
		border-radius: 5px  5px  5px  5px;
		padding: 0 12px;
		color: #666;
		background: #F4F4F4;
		width: 100%;
		font-size: 16px;
		min-width: 50%;
		height: 40px;
	}
	.add-update-preview .el-input-number {
		text-align: left;
		width: 100%;
	}
	.add-update-preview .el-input-number /deep/ .el-input__inner {
		text-align: left;
		border: 2px solid #000000;
		border-radius: 5px  5px  5px  5px;
		padding: 0 12px;
		color: #666;
		background: #F4F4F4;
		width: 100%;
		font-size: 16px;
		min-width: 50%;
		height: 40px;
	}
	.add-update-preview .el-input-number /deep/ .is-disabled .el-input__inner {
		text-align: left;
		border: 2px solid #000000;
		border-radius: 5px  5px  5px  5px;
		padding: 0 12px;
		color: #666;
		background: #F4F4F4;
		width: 100%;
		font-size: 16px;
		min-width: 50%;
		height: 40px;
	}
	.add-update-preview .el-input-number /deep/ .el-input-number__decrease {
		display: none;
	}
	.add-update-preview .el-input-number /deep/ .el-input-number__increase {
		display: none;
	}
	.add-update-preview .el-select {
		width: 100%;
	}
	.add-update-preview .el-select /deep/ .el-input__inner {
		border: 2px solid #000000;
		border-radius: 5px  5px  5px  5px;
		padding: 0 12px;
		color: #666;
		background: #F4F4F4;
		width: 100%;
		font-size: 16px;
		min-width: 50%;
		height: 40px;
	}
	.add-update-preview .el-select /deep/ .is-disabled .el-input__inner {
		border: 2px solid #000000;
		border-radius: 5px  5px  5px  5px;
		padding: 0 12px;
		color: #666;
		background: #F4F4F4;
		width: 100%;
		font-size: 16px;
		min-width: 50%;
		height: 40px;
	}
	.add-update-preview .el-date-editor {
		width: 100%;
	}
	.add-update-preview .el-date-editor /deep/ .el-input__inner {
		border: 2px solid #000000;
		border-radius: 5px  5px  5px  5px;
		padding: 0 30px;
		color: #666;
		background: #F4F4F4;
		width: 100%;
		font-size: 16px;
		min-width: 50%;
		height: 40px;
	}
	.add-update-preview .el-date-editor /deep/ .el-input__inner[readonly="readonly"] {
		border: 2px solid #000000;
		border-radius: 5px  5px  5px  5px;
		padding: 0 30px;
		color: #666;
		background: #F4F4F4;
		width: 100%;
		font-size: 16px;
		min-width: 50%;
		height: 40px;
	}
	.add-update-preview .viewBtn {
		border: 2px solid #000000;
		cursor: pointer;
		border-radius: 0px;
		padding: 0 15px;
		margin: 0 20px 0 0;
		color: #666;
		background: #F4F4F4;
		width: auto;
		font-size: 15px;
		line-height: 40px;
		text-align: left;
		height: 40px;
		.iconfont {
			margin: 0 2px;
			color: #666;
			font-size: 16px;
			height: 34px;
		}
	}
	.add-update-preview .viewBtn:hover {
		opacity: 0.8;
	}
	.add-update-preview .downBtn {
		border: 2px solid #000000;
		cursor: pointer;
		border-radius: 0px;
		padding: 0 15px;
		margin: 0 20px 0 0;
		color: #666;
		background: #F4F4F4;
		width: auto;
		font-size: 15px;
		line-height: 40px;
		text-align: left;
		height: 40px;
		.iconfont {
			margin: 0 2px;
			color: #666;
			font-size: 16px;
			height: 34px;
		}
	}
	.add-update-preview .downBtn:hover {
		opacity: 0.8;
	}
	.add-update-preview .unBtn {
		border: 2px solid #000000;
		cursor: pointer;
		border-radius: 0px;
		padding: 0 15px;
		margin: 0 20px 0 0;
		color: #666;
		background: #F4F4F4;
		width: auto;
		font-size: 15px;
		line-height: 40px;
		text-align: left;
		height: 40px;
		.iconfont {
			margin: 0 2px;
			color: #fff;
			display: none;
			font-size: 14px;
			height: 34px;
		}
	}
	.add-update-preview .unBtn:hover {
		opacity: 0.8;
	}
	.add-update-preview /deep/ .el-upload--picture-card {
		background: transparent;
		border: 0;
		border-radius: 0;
		width: auto;
		height: auto;
		line-height: initial;
		vertical-align: middle;
	}
	
	.add-update-preview /deep/ .upload .upload-img {
		border: 2px solid #000000;
		cursor: pointer;
		border-radius: 5px 5px 5px 5px;
		color: #666;
		background: #F4F4F4;
		width: 90px;
		font-size: 24px;
		line-height: 60px;
		text-align: center;
		height: 60px;
	}
	
	.add-update-preview /deep/ .el-upload-list .el-upload-list__item {
		border: 2px solid #000000;
		cursor: pointer;
		border-radius: 5px 5px 5px 5px;
		color: #666;
		background: #F4F4F4;
		width: 90px;
		font-size: 24px;
		line-height: 60px;
		text-align: center;
		height: 60px;
	}
	
	.add-update-preview /deep/ .el-upload .el-icon-plus {
		border: 2px solid #000000;
		cursor: pointer;
		border-radius: 5px 5px 5px 5px;
		color: #666;
		background: #F4F4F4;
		width: 90px;
		font-size: 24px;
		line-height: 60px;
		text-align: center;
		height: 60px;
	}
	.add-update-preview /deep/ .el-upload__tip {
		color: #666;
		font-size: 15px;
	}
	
	.add-update-preview .el-textarea /deep/ .el-textarea__inner {
		border:  2px solid #000000;
		border-radius: 0px;
		padding: 12px;
		color: #666;
		background: #F4F4F4;
		width: auto;
		font-size: 14px;
		min-width: 1200px;
		height: 208px;
	}
	.add-update-preview .el-textarea /deep/ .el-textarea__inner[readonly="readonly"] {
				border:  2px solid #000000;
				border-radius: 0px;
				padding: 12px;
				color: #666;
				background: #F4F4F4;
				width: auto;
				font-size: 14px;
				min-width: 1200px;
				height: 208px;
			}
	.add-update-preview .el-form-item.btn {
		padding: 0;
		margin: 20px 0 0;
		.btn1 {
			border: 0px solid #ccc;
			cursor: pointer;
			border-radius: 4px;
			padding: 0 10px;
			margin: 0 10px 0 0;
			color: #fff;
			background: #66D5F8;
			width: auto;
			font-size: 16px;
			min-width: 110px;
			height: 40px;
			.iconfont {
				margin: 0 2px;
				color: #fff;
				display: none;
				font-size: 14px;
				height: 40px;
			}
		}
		.btn1:hover {
			opacity: 0.8;
		}
		.btn2 {
			border: 0px solid #ccc;
			cursor: pointer;
			border-radius: 4px;
			padding: 0 10px;
			margin: 0 10px 0 0;
			color: #fff;
			background: #EF8E6A;
			width: auto;
			font-size: 16px;
			min-width: 110px;
			height: 40px;
			.iconfont {
				margin: 0 2px;
				color: #fff;
				display: none;
				font-size: 14px;
				height: 34px;
			}
		}
		.btn2:hover {
			opacity: 0.8;
		}
		.btn3 {
			border: 0px solid #ccc;
			cursor: pointer;
			border-radius: 4px;
			padding: 0 10px;
			margin: 0 10px 0 0;
			color: #fff;
			background: #348CB4;
			width: auto;
			font-size: 16px;
			min-width: 110px;
			height: 40px;
			.iconfont {
				margin: 0 2px;
				color: #fff;
				display: none;
				font-size: 14px;
				height: 40px;
			}
		}
		.btn3:hover {
			opacity: 0.8;
		}
		.btn4 {
			border: 2px solid #57CAFF;
			cursor: pointer;
			border-radius: 4px;
			padding: 0 10px;
			margin: 0 10px 0 0;
			color: #57CAFF;
			background: #fff;
			width: auto;
			font-size: 16px;
			min-width: 110px;
			height: 40px;
			.iconfont {
				margin: 0 2px;
				color: #fff;
				display: none;
				font-size: 14px;
				height: 40px;
			}
		}
		.btn4:hover {
			opacity: 0.8;
		}
		.btn5 {
			border: 2px solid #57CAFF;
			cursor: pointer;
			border-radius: 4px;
			padding: 0 10px;
			margin: 0 10px 0 0;
			color: #57CAFF;
			background: #fff;
			width: auto;
			font-size: 16px;
			min-width: 110px;
			height: 40px;
			.iconfont {
				margin: 0 2px;
				color: #fff;
				display: none;
				font-size: 14px;
				height: 40px;
			}
		}
		.btn5:hover {
			opacity: 0.8;
		}
	}
</style>
