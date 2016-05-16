# demo
一些实用JS 函数
//竞彩足球 分组
var getPosition = function(n) {
	n = -1 * Number(n);
	var zsArr = n > 0 ? [1, 0, -1] : [1];
	var zfArr = n < 0 ? [1, 0, -1] : [-1];
	if (Math.abs(n) === 1) {
		var zsArr = n > 0 ? [1, 0] : [1];
		var zfArr = n < 0 ? [0, -1] : [-1];
	} else {
		var zsArr = n > 0 ? [1, 0, -1] : [1];
		var zfArr = n < 0 ? [1, 0, -1] : [-1];
	}
	var spArr = [
		//按照比分进行分组
		//胜平负,让球胜平负净胜球,比分,半全场,总进球,备用
		[['spf_3'], [1 - 0 - n], ['bf_10'], ['bqc_33', 'bqc_13'], ['zjq_1'], [0]],
		[['spf_3'], [2 - 0 - n], ['bf_20'], ['bqc_33', 'bqc_13'], ['zjq_2'], [0]],
		[['spf_3'], [2 - 1 - n], ['bf_21'], ['bqc_33', 'bqc_13', 'bqc_03'], ['zjq_3'], [0]],
		[['spf_3'], [3 - 0 - n], ['bf_30'], ['bqc_33', 'bqc_13'], ['zjq_3'], [0]],
		[['spf_3'], [3 - 1 - n], ['bf_31'], ['bqc_33', 'bqc_13', 'bqc_03'], ['zjq_4'], [0]],
		[['spf_3'], [3 - 2 - n], ['bf_32'], ['bqc_33', 'bqc_13', 'bqc_03'], ['zjq_5'], [0]],
		[['spf_3'], [4 - 0 - n], ['bf_40'], ['bqc_33', 'bqc_13'], ['zjq_4'], [0]],
		[['spf_3'], [4 - 1 - n], ['bf_41'], ['bqc_33', 'bqc_13', 'bqc_03'], ['zjq_5'], [0]],
		[['spf_3'], [4 - 2 - n], ['bf_42'], ['bqc_33', 'bqc_13', 'bqc_03'], ['zjq_6'], [0]],
		[['spf_3'], [5 - 0 - n], ['bf_50'], ['bqc_33', 'bqc_13'], ['zjq_5'], [0]],
		[['spf_3'], [5 - 1 - n], ['bf_51'], ['bqc_33', 'bqc_13', 'bqc_03'], ['zjq_6'], [0]],
		[['spf_3'], [5 - 2 - n], ['bf_52'], ['bqc_33', 'bqc_13', 'bqc_03'], ['zjq_7'], [0]],
		[['spf_3'], zsArr, ['bf_3A'], ['bqc_33', 'bqc_13', 'bqc_03'], ['zjq_6', 'zjq_7'], [0]],//胜其他
		[['spf_1'], [0 - 0 - n], ['bf_00'], ['bqc_11'], ['zjq_0'], [0]],
		[['spf_1'], [1 - 1 - n], ['bf_11'], ['bqc_31', 'bqc_11', 'bqc_01'], ['zjq_2'], [0]],
		[['spf_1'], [2 - 2 - n], ['bf_22'], ['bqc_31', 'bqc_11', 'bqc_01'], ['zjq_4'], [0]],
		[['spf_1'], [3 - 3 - n], ['bf_33'], ['bqc_31', 'bqc_11', 'bqc_01'], ['zjq_6'], [0]],
		[['spf_1'], [-1 * n], ['bf_1A'], ['bqc_31', 'bqc_11', 'bqc_01'], ['zjq_7'], [0]],//平其他
		[['spf_0'], [0 - 1 - n], ['bf_01'], ['bqc_10', 'bqc_00'], ['zjq_1'], [1]],
		[['spf_0'], [0 - 2 - n], ['bf_02'], ['bqc_10', 'bqc_00'], ['zjq_2'], [1]],
		[['spf_0'], [1 - 2 - n], ['bf_12'], ['bqc_30', 'bqc_10', 'bqc_00'], ['zjq_3'], [1]],
		[['spf_0'], [0 - 3 - n], ['bf_03'], ['bqc_10', 'bqc_00'], ['zjq_3'], [1]],
		[['spf_0'], [1 - 3 - n], ['bf_13'], ['bqc_30', 'bqc_10', 'bqc_00'], ['zjq_4'], [1]],
		[['spf_0'], [2 - 3 - n], ['bf_23'], ['bqc_30', 'bqc_10', 'bqc_00'], ['zjq_5'], [1]],
		[['spf_0'], [0 - 4 - n], ['bf_04'], ['bqc_10', 'bqc_00'], ['zjq_4'], [1]],
		[['spf_0'], [1 - 4 - n], ['bf_14'], ['bqc_30', 'bqc_10', 'bqc_00'], ['zjq_5'], [1]],
		[['spf_0'], [2 - 4 - n], ['bf_24'], ['bqc_30', 'bqc_10', 'bqc_00'], ['zjq_6'], [1]],
		[['spf_0'], [0 - 5 - n], ['bf_05'], ['bqc_10', 'bqc_00'], ['zjq_5'], [1]],
		[['spf_0'], [1 - 5 - n], ['bf_15'], ['bqc_30', 'bqc_10', 'bqc_00'], ['zjq_6'], [1]],
		[['spf_0'], [2 - 5 - n], ['bf_25'], ['bqc_30', 'bqc_10', 'bqc_00'], ['zjq_7'], [1]],
		[['spf_0'], zfArr, ['bf_0A'], ['bqc_30', 'bqc_10', 'bqc_00'], ['zjq_6', 'zjq_7'], [1]]//负其他
	];
	return spArr;
};
//生成对阵 例如[[1,1.1],[2]] 会生成[[1,2],[1.1,2]]
var match = function(A) {
	//this.gg是每组比赛的对象
	//用以生成每组比赛的对阵
	var B = 0, C = [], D = [], _;
	tool(A, B);
	function tool(A, B) {
		if (_ || B >= A.length) {
			C.push(D.slice());
			D.length = B - 1
		} else {
			var E = A[B];
			for (var G = 0, F = E.length; G < F; G++) {
				D.push(E[G]);
				tool(A, B + 1)
			}
			if (B)
				D.length = B - 1
		}
	}
	return C
};
//该函数为分组函数例如s = [1,2,3];n=2;得到的结果是[[1,2],[1,3],[2,3]]
var zuhe = function(s,n){
	var r = [];
	for (var i=0;i<Math.pow(2, s.length);i++){
		var a = 0;
		var b = [];
		for (var j=0;j<s.length;j++){
			if (i>>j&1){
				a++;
				b[b.length]=(s[j]);
			}
		}
		if (a==n){
			r[r.length] = (b);
		}
	}
	return r;
}
/**
*观察者模式
*中继调用分发
example：
var obj = { name: 'sam' };
    mediator.installTo(obj);
	//注册
    obj.subscribe('nameChange', function(arg){
            console.log(this.name);//this instanceof obj --> true
    });
    //发布--触发注册时function
    obj.publish('nameChange',arg); or mediator.publish('nameChange',arg)//tigger,arg 可以不用传
*/
var mediator = (function(){
	var subscribe = function(channel, fn){
		if (!mediator.channels[channel]) mediator.channels[channel] = [];
		mediator.channels[channel].push({ context: this, callback: fn });
		return this;
	},
	remove = function(channel){
		if (!mediator.channels[channel]) return this;
		delete mediator.channels[channel];
		return this;
	},
	publish = function(channel){
		if (!mediator.channels[channel]) return this;
		var args = Array.prototype.slice.call(arguments, 1);//从第一个下标开始截取，第0个为 channl值
		for (var i = 0, l = mediator.channels[channel].length; i < l; i++) {
			var subscription = mediator.channels[channel][i];
			subscription.callback.apply(subscription.context, args);
		}
		return this;
	};
	return {
		channels: {},
		publish: publish,
		subscribe: subscribe,
		remove: remove,
		installTo: function(obj){
			obj.subscribe = subscribe;
			obj.removeSubscribe = remove;
			obj.publish = publish;
		}
	};
 
}());
