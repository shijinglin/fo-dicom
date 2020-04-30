Fork From https://github.com/fo-dicom/fo-dicom , 相关介绍请看原始连接。

---

分支修改履历：


### 2020-4-30 优化字符集

#### 1. 优化字符集

   *将整个解决方案中，没有直接使用DicomEncoding.Default作为默认值的地方都改成了DicomEncoding.Default ，便于统一指定字符集。*

#### 2. 在DicomDataset中增加了BuildDefaultEncoding方法
* 创建完所有标签之后主动调用一下， 如果标签列表中没有包含SpecificCharacterSet，则用默认字符集进行补充，明确指定过就可以不用调用了。
* 首次获取数据的时候会自动调用BuildDefaultEncoding，如果优先从所有标签中寻找SpecificCharacterSet来恢复默认字符集，然后再转换取值。

   *没有太过深入的去合理化维护字符集，外挂式的写了个方法按需调用，减少程序使用时的额外处理，仁者见仁，不喜勿喷！*
   


### 2020-4-29 优化字符集

#### 1. 默认字符集变量DicomEncoding.Default改成可修改的属性

   *原本默认是ASCII，对中文支持不足，使用方法：DicomEncoding.Default = Encoding.UTF8;*

#### 2. 优化DicomDataset取值
* 原本GetValue<string>和GetSingleValue<string>有bug，没有使用到字符集回转。
* GetValue<string>和GetSingleValue<string>两个方法增加了Encoding参数，方便直接做字符转换。

   *用于不能直接修改DicomEncoding.Default的情况，如：写入字符集和获取到的Dicom字符集不一致，或同时对接不同字符集的Dicom时。*
   
