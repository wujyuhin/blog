From datetime import datetime

1. 常见日期有
	1608085848     # int 十位数表示'2020 年 12 月 16 日 10:30:48'的时间戳，记录的是从 1970 年 1 月 1 日凌晨开始的秒数。
	'2020-12-16 10:31:08'		# 字符串
	'2020-12-16 10:31:08.132465'	# 字符串 
	'2020 年 12 月 16 日 10:30:48'		# 字符串
	'11/Nov/20 20:00:31: 36'  	# 字符串

2. Format 语法设置
	%Y 表示年	%b 表示月英文简写
	%m 表示月	%B  表示月英文全拼
	%d 表示天	% #m 表示去掉最前面的 0 如 07 -> 7
	%H 表示小时
	%M 表示分钟
	%S 表示秒

3. 统一转为 datetime 格式
	1)数字 -> datetime
		Datetime.Fromtimestamp (2541236595)
	2)字符串 -> datetime
		datetime.Strptime ('2020-06-16 10:31:08','%Y-%m-%d %H:%M:%S')  【注】str p time
4. 统一转为数字格式
	1)字符串/datetime -> 数字
		time = datetime.Striptime ('2020-06-16 10:31:08','%Y-%m-%d %H:%M:%S')
		Time.Timestamp ()
	
5. 统一转为字符串格式
	1)数字/datetime -> 字符串
		Time = datetime.Fromtimestamp (2541236595)
		Time.Strftime ('%Y-%m-%d %H:%M:%s')  【注】str f time
		
