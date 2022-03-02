---
title: 如何在C语言中使用tensorflow（四）实例
date: 2020-05-16 20:21:00
categories:
	-机器学习
	-工程化
---

本文主要通过TF_SessionRun的方式输出字符串内容：

```
#include<stdlib.h>
#include<stdio.h>
#include<string.h>
#include<tensorflow/c/c_api.h>

int main( int argc, char ** argv ) 
{
  TF_Graph * graph = TF_NewGraph();
  TF_SessionOptions * options = TF_NewSessionOptions();
  TF_Status * status = TF_NewStatus();
  TF_Session * session = TF_NewSession( graph, options, status );
  char hello[] = "Hello TensorFlow!";
  TF_Tensor * tensor = TF_AllocateTensor( TF_STRING, 0, 0, 8 + TF_StringEncodedSize( strlen( hello ) ) );
  TF_Tensor * tensorOutput;
  TF_OperationDescription * operationDescription = TF_NewOperation( graph, "Const", "hello" );
  TF_Operation * operation; 
  struct TF_Output output;

  TF_StringEncode( hello, strlen( hello ), 8 + ( char * ) TF_TensorData( tensor ), TF_StringEncodedSize( strlen( hello ) ), status );
  memset( TF_TensorData( tensor ), 0, 8 );
  TF_SetAttrTensor( operationDescription, "value", tensor, status );
  TF_SetAttrType( operationDescription, "dtype", TF_TensorType( tensor ) );
  operation = TF_FinishOperation( operationDescription, status );

  output.oper = operation;
  output.index = 0;

  TF_SessionRun( session, 0,
                 0, 0, 0,  // Inputs
                 &output, &tensorOutput, 1,  // Outputs
                 &operation, 1,  // Operations
                 0, status );

  printf( "status code: %i\n", TF_GetCode( status ) );
  printf( "%s\n", ( ( char * ) TF_TensorData( tensorOutput ) ) + 9 );

  TF_CloseSession( session, status );
  TF_DeleteSession( session, status );
  TF_DeleteStatus( status );
  TF_DeleteSessionOptions( options );  

  return 0;
}
```


将代码替换到test.c当中，编译生成可执行文件test。

```
./test
2020-11-16 19:58:37.850140: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2020-11-16 19:58:37.874392: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 3000000000 Hz
2020-11-16 19:58:37.874637: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x559021926b60 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2020-11-16 19:58:37.874654: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
status code: 0
Hello TensorFlow!
```


从可执行文件的输出结果发现，输出包含LOG信息，LOG信息通过宏TF_CPP_MIN_LOG_LEVEL确定，具体取值及意义如下表所示。

| 编号 | 含义                             |
| ---- | -------------------------------- |
| 0    | 默认值，输出所有信息             |
| 1    | 屏蔽通知信息                     |
| 2    | 屏蔽通知信息和警告信息           |
| 3    | 屏蔽通知信息、警告信息和报错信息 |



因此可以根据要求将TF_CPP_MIN_LOG_LEVEL设置为合理值

```
export TF_CPP_MIN_LOG_LEVEL='2'
./test
status code: 0
Hello TensorFlow!
```

