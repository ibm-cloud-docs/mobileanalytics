---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 设置警报
{: #alerts}

## 使用 Mobile Analytics 设置警报 

您可以在 {{site.data.keyword.mobileanalytics_short}} 控制台中的警报定义内设置阈值，以更好地监视活动。

您可以配置阈值，当超过阈值时，触发器便会触发警报以向 {{site.data.keyword.mobileanalytics_short}} 控制台监视器通知此情况。已触发的警报可以显示在控制台中，也可以由定制 webhook 进行处理。<!-- This feature provides a proactive means of detecting app log errors, server log errors, extended periods of network latency, and authentication failures.--> 此功能能够主动检测应用程序日志错误和应用程序崩溃服务器日志错误。响应式阈值和警报使您不必筛查数据，或者设置大范围的阈值。

## 为应用程序日志创建警报定义
{: #alert-def-client-logs notoc}

您可以基于应用程序日志创建警报定义。

在此示例中，您将使用应用程序日志数据来创建警报定义。该警报会监控在过去 5 分钟内收到的所有应用程序日志，并且每 5 分钟继续检查一次，直到该警报定义被禁用或删除。如果设备发送了 3 个或更多个具有相同应用程序名称和版本的应用程序错误日志，那么将会触发警报。

1. 在 {{site.data.keyword.mobileanalytics_short}} 控制台中，单击**定义**以转至“警报定义”页面。
2. 单击**创建警报**以创建警报。
3. 提供以下值：
	* 警报名称：应用程序日志的警报
	* 消息：错误消息警报
	* 查询频率：5 分钟
	* 事件类型：应用程序日志
		* 属性：日志级别
			* 值：错误
			* 阈值
				* 阈值类型：应用程序实例的总计

					**注**：如果您选择“应用程序的平均值”选项，那么会按设备数来计算应用程序日志平均值。例如，如果您有两个设备，其中一个设备发送六个应用程序日志，而另一个设备发送三个应用程序日志，那么平均值为 4.5 个应用程序日志。
				* 运算符：大于或等于 3
	
	<!-- insert alert definition tab image? -->

4. 单击**下一步**，然后提供以下值：
	* 方法：仅限分析控制台

		**注**：如果您想要额外发送具有 JSON 有效内容的 POST 消息到您定制的 URL，请选择“分析控制台和网络 Post”选项。如果选择此选项，那么以下字段可用：
		* 网络 Post URL
        * 标头
        * 认证类型
5. 单击**保存**。

您已创建警报定义，在应用程序日志数达到您的阈值，即 3 个或更多错误日志时，每 5 分钟触发一次警报。

## 为应用程序崩溃创建警报定义
{: #alert-def-app-crash notoc}

您可以基于应用程序崩溃来创建警报定义。

在此示例中，您将使用应用程序崩溃数据来创建警报定义。该警报会监控在过去 2 分钟内出现的所有应用程序崩溃，并且每 2 分钟继续检查一次，直到该警报定义被禁用或删除。对于出现 5 次或以上崩溃事件的应用程序，将触发警报。
有关应用程序崩溃的更多信息，请参阅[应用程序崩溃](#app_crash)。

1. 在 {{site.data.keyword.mobileanalytics_short}} 控制台中，单击**定义**以显示“警报定义”页面。
2. 单击**创建警报**。 
3. 提供以下值：
	* 警报名称：应用程序崩溃的警报
	* 消息：应用程序崩溃警报
	* 查询频率：应用程序崩溃
		* 查询频率：2 分钟
	* 事件类型：应用程序崩溃
		* 应用程序名称：任何应用程序
		* 应用程序版本：任何版本
    * 阈值
      * 阈值类型：崩溃计数
      * 运算符：大于或等于 5
4. 单击**分发方法**选项卡并提供以下值：
  * 方法：仅限分析控制台

    **注**：如果您想要额外发送具有 JSON 有效内容的 POST 消息到您定制的 URL，请选择**分析控制台和网络 Post** 选项。如果选择此选项，那么以下字段可用：
      * 网络 Post URL（必需）
      * 标头（可选）
      * 认证类型（必需）
5. 单击**保存**。

## 管理警报定义
{: #managing-alert-definitions notoc}

在此示例中，您将通过“警报管理”页面来管理警报定义。

1. 在 {{site.data.keyword.mobileanalytics_short}} 控制台中，单击**日志**。此操作会打开“警报日志”页面。
2. 可选：切换**启用**列下的复选框，以启用或禁用特定警报定义。
3. 可选：如果您想要创建警报定义的副本并更改一些值，请单击**复制**图标。
4. 可选：如果您想要编辑警报定义，请单击**画笔**图标。
5. 可选：如果您想要删除警报定义，请单击**废纸篓**图标。

## 查看警报详细信息
{: #viewing-alert-details notoc}

在此示例中，您将在“警报日志”页面中查看已触发警报的详细信息。

1. 在 {{site.data.keyword.mobileanalytics_short}} 控制台中，单击**日志**。此操作会打开“警报日志”页面。
2. 单击任意警报的 **+** 图标。该操作会显示**警报定义**和**警报实例**部分。

    **注**：如果未删除或修改相应的警报定义，那么您可以通过单击**编辑警报**，来编辑警报定义。否则，无法使用**编辑警报**按钮，且会显示下列消息：

    `此警报定义已修改或删除。`

3. 可选：选择警报并单击**废纸篓**图标，以删除警报。
