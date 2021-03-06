# AddressSelector

一个 Android 版京东手机客户端（当前版本V1..0.0 ）风格的级联地址选择器。
     ![image](https://github.com/smartTop/AddressSelector/blob/master/screenshots/screenshot1.gif)
## 添加依赖

在`build.gradle` 中：

    dependencies {
        ...
       compile 'com.smartTop:address-selector:1.0.5'
    }
    
## 使用方法

    AddressSelector selector = new AddressSelector(context);
    selector.setOnAddressSelectedListener(new AddressSelector.OnAddressSelectedListener() {
        @Override
        public void onAddressSelected(Province province, City city, County county, Street street) {
            // blahblahblah
        }
    });
            
    View view = selector.getView();
    content.addView(view);

    默认的样式
![image](https://github.com/smartTop/AddressSelector/blob/master/screenshots/screenshort4.png)


    自定义样式

    //设置字体的大小

 selector.setTextSize(14);

 //设置指示器的背景颜色

   selector.setIndicatorBackgroundColor("#00ff00");

   或

    selector.setIndicatorBackgroundColor(android.R.color.holo_orange_light);

    //设置字体的背景

    selector.setBackgroundColor(android.R.color.holo_red_light);

    //设置字体获得焦点的颜色

    selector.setTextSelectedColor(android.R.color.holo_orange_light);

    //设置字体没有获得焦点的颜色

    selector.setTextUnSelectedColor(android.R.color.holo_blue_light);

    //自定义dialog的样式

     dialog.setTextSize(14);//设置字体的大小
     dialog.setIndicatorBackgroundColor(android.R.color.holo_orange_light);//设置指示器的颜色
     dialog.setTextSelectedColor(android.R.color.holo_orange_light);//设置字体获得焦点的颜色
     dialog.setTextUnSelectedColor(android.R.color.holo_blue_light);//设置字体没有获得焦点的颜色

     效果图
![image](https://github.com/smartTop/AddressSelector/blob/master/screenshots/screenshort5.png)


### BottomDialog  弹出地址选择器的dialog的用法及回调

    BottomDialog dialog = new BottomDialog(context);
    dialog.setOnAddressSelectedListener(this);
    dialog.setDialogDismisListener(this);
    dialog.show();

       @Override
        public void onAddressSelected(Province province, City city, County county, Street street) {
            provinceCode = (province == null ? "" : province.code);
            cityCode = (city == null ? "" : city.code);
            countyCode = (county == null ? "" : county.code);
            streetCode = (street == null ? "" : street.code);
            LogUtil.d("数据", "省份id=" + provinceCode);
            LogUtil.d("数据", "城市id=" + cityCode);
            LogUtil.d("数据", "乡镇id=" + countyCode);
            LogUtil.d("数据", "街道id=" + streetCode);
            String s = (province == null ? "" : province.name) + (city == null ? "" : city.name) + (county == null ? "" : county.name) +
                    (street == null ? "" : street.name);
            tv_selector_area.setText(s);
            if (dialog != null) {
                dialog.dismiss();
            }
        }

        @Override
        public void dialogclose() {
            if(dialog!=null){
                dialog.dismiss();
            }
        }
###
有朋友问，怎么使用自己的数据源，这里我说明一下，因为我的数据库里的地址表，省，市，区，县，镇，都是用同一个表，根据parentId来查询的。

想用自己的数据源，就需要把自己的数据源里，各个字段与我的数据源里字段一一对应(id, parentId, code, name),分别对应的中文意思(id,父id(可根据父id查询下一级),地址编码,中文名字)

然后在你的项目里的assets目录下，放上你的数据库，名字一定是"address.db".

    如果你用的是android studio 应该放在
 ![image](https://github.com/smartTop/AddressSelector/blob/master/screenshots/screenshort2.png)
###
在源数据库里要添加一个数据
 AdressBean.ChangeRecordsBean changeRecordsBean = new AdressBean.ChangeRecordsBean();

        changeRecordsBean.parentId = 0;

        changeRecordsBean.name = "测试省";

        changeRecordsBean.id = 35;

        addressDictManager.inserddress(changeRecordsBean);
![image](https://github.com/smartTop/AddressSelector/blob/master/screenshots/screenshort3.png)
###
 还可以进行已下操作 增加一个数据 inserddress(AdressBean.ChangeRecordsBean adress)  增加一个集合insertAddress(List<AdressBean.ChangeRecordsBean> list)

 更新数据 updateAddressInfo(AdressBean.ChangeRecordsBean adress)

 查找数据 getAddressList()

 获取省市列表 getProvinceList()

 根据省市id 获取城市列表 getCityList(int  provinceId)

 获取城市对应的区，乡镇列表 getCountyList(int cityId)

 获取区，乡镇对应的街道列表 getStreetList(int countyId)

  查找消息临时列表中是否存在这一条记录  isExist()
## 关于我

**smartTop**

- 博客 http://blog.csdn.net/qq_30740239
- gitHub https://github.com/smartTop/AddressSelector
- QQ 1273436145
