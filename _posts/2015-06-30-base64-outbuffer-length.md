---
layout: post
category: "android"
title: "C语言Base64输出buffer大小计算"
tags: ["C语言,Base64,输出,buffer,大小"]
---
####一、Base64编码过程
将3字节(3×8=24)分块成4字节(4×6=24,高位补0)，即3个字节输入转换成4个字节输出。  
因此，输入字符串长度如果不是3的整数倍，则需要在末尾补1或2个=。  

####二、C语言实现计算输出buffer(char *)大小计算方法

	/**
	 * 取补的'='长度
	 */
	unsigned int get_base64_output_padd_len(const unsigned char * input) {
		const unsigned char *ptr = input;
		ptr = ptr + strlen(input);
		unsigned int pad_len = 0;
		unsigned int i = 0;
		while (i < 3) { //补'='的长度只可能是1或2
			if (*ptr == 61) {
				pad_len++;
			}
			ptr--;
			i++;
		}
		return pad_len;
	}

	/**
	 * 获取base64输出buffer所需的长度
	 */
	unsigned int get_base64_output_len(const unsigned char * input,
			unsigned int type) {
		unsigned int count = 0;
		if (type == 0) { //根据原始输入字符串计算编码后字符串的长度
			unsigned int len = strlen(input);
			unsigned int pad = (len % 3 == 0) ? 0 : (3 - len % 3);
			count = ((len + pad) * 8 / 6);
		} else { //根据编码后的字符串计算编码前字符串的长度（补位后的）
			const unsigned char *ptr = input;
			unsigned char tmp;
			unsigned int total = 0;
			while ((tmp = *ptr) != '\0') { //过滤'\n'
				if (tmp != '\n') {
					total++;
				}
				ptr++;
			}
			unsigned int pad_len = get_base64_output_padd_len(input);
			count = (total * 6 / 8) - pad_len;
		}
		return count;
	}

####三、编码中有\n字符的情况
JAVA base64的某些实现版本，编码后的字符串中可能带有"\n"字符（方便输出时查看），getOutputLen就不再准确了，需要过滤掉"\n"字符。

	System.out.println("getOutputLen:"+getOutputLen(input));//根据原始输入字符串计算编码后字符串的长度为1144
	String result = Base64.encodeToString(input.getBytes("UTF-8"), 0);//对字符串按Base64编码
	System.out.println("result Len:"+result.length());//实际的result长度发现为1160
	result=result.replaceAll("\n", "");//因为它附加了\n字符，需要滤\n字符
	System.out.println("real result Len:"+result.length());//输出1144，这就对了！

（完~）
