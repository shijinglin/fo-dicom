Fork From https://github.com/fo-dicom/fo-dicom , 相关介绍请看原始连接。

---

分支修改履历：

### 2020-4-29 优化字符集

#### 1. 默认字符集变量DicomEncoding.Default改成可修改的属性

   *原本默认是ASCII，对中文支持不足，使用方法：DicomEncoding.Default = Encoding.UTF8;*

#### 2. 优化DicomDataset取值
* 原本GetValue<string>和GetSingleValue<string>有bug，没有使用到字符集回转。
* GetValue<string>和GetSingleValue<string>两个方法增加了Encoding参数，方便直接做字符转换。

   *用于不能直接修改DicomEncoding.Default的情况，如：写入字符集和获取到的Dicom字符集不一致，或同时对接不同字符集的Dicom时。*
   
