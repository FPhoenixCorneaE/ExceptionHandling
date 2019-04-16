**问题出现背景：**

- 数据库查询使用的是**GreenDao 3.2.2**

- 由于历史记录可以重复，除了autoincrement的id以外并没有Unique的属性，所以获取收藏列表时需要做去重处理，但是GreenDao并没有提供可直接调用的去重方法，虽然找到了distinct()方法，但GreenDao对distince()的描述是：Use a SELECT DISTINCT to avoid duplicate entities returned, e.g. when doing joins. 意思应该是联表查询去重，在这里并不适用，这里是单表。


**实体类：**
```java
package com.galanz.oven.greendao.bean;

import android.os.Parcel;
import android.os.Parcelable;

import org.greenrobot.greendao.annotation.Entity;
import org.greenrobot.greendao.annotation.Generated;
import org.greenrobot.greendao.annotation.Id;

/**
 * 历史记录
 *
 * @author wkz
 * @date 2019/4/9 10:33
 */
@Entity
public class IotHistoryBean implements Parcelable {

    @Id(autoincrement = true)
    private Long id;
    /**
     * 添加时间
     */
    private long createTime;
    /**
     * 菜谱id
     */
    private String recipeId;
    /**
     * 菜谱名称
     */
    private String recipeName;
    /**
     * 菜谱图片
     */
    private String recipeImgUrl;
    /**
     * 菜谱本地资源图片
     */
    private int recipeImgRes;
    /**
     * 烹饪火力
     */
    private String firepower;
    /**
     * 火力单位
     */
    private String firepowerUnit;
    /**
     * 食材重量
     */
    private String weight;
    /**
     * 重量单位
     */
    private String weightUnit;
    /**
     * 烹饪温度
     */
    private String cookingTemp;
    /**
     * 烹饪时间
     */
    private String cookingTime;
    /**
     * 菜谱配置参数
     */
    private String recipeConfig;
    /**
     * 预约烹饪火力
     */
    private String preAppointFirepower;
    /**
     * 预约食材重量
     */
    private String preAppointWeight;
    /**
     * 预约烹饪温度
     */
    private String preAppointCookingTemp;
    /**
     * 预约烹饪时间
     */
    private String preAppointCookingTime;
    /**
     * 预约菜谱配置参数
     */
    private String preAppointRecipeConfig;
    /**
     * 是否需要预热
     */
    private boolean isNeedPreHeated;
    /**
     * 预热温度
     */
    private String preHeatTemp;
    /**
     * 是否正常的烹饪
     */
    private boolean isNormalCooking;
    /**
     * 最近烹饪时间
     */
    private long normalCookingTime;
    /**
     * 是否预约
     */
    private boolean isPreAppoint;
    /**
     * 预约时间
     */
    private long preAppointTime;
    /**
     * 是否收藏
     */
    private boolean isFavorite;
    /**
     * 收藏时间
     */
    private long favoriteTime;
    /**
     * 是否同步收藏
     */
    private boolean hasSynchronizedFavorite;
    /**
     * 同步收藏时间
     */
    private long synchronizedFavoriteTime;
    /**
     * 是否同步预约
     */
    private boolean hasSynchronizedPreAppoint;
    /**
     * 同步预约时间
     */
    private long synchronizedPreAppointTime;
    /**
     * 是否同步烹饪
     */
    private boolean hasSynchronizedCooking;
    /**
     * 同步烹饪时间
     */
    private long synchronizedCookingTime;

    @Override
    public int describeContents() {
        return 0;
    }

    @Override
    public void writeToParcel(Parcel dest, int flags) {
        dest.writeValue(this.id);
        dest.writeLong(this.createTime);
        dest.writeString(this.recipeId);
        dest.writeString(this.recipeName);
        dest.writeString(this.recipeImgUrl);
        dest.writeInt(this.recipeImgRes);
        dest.writeString(this.firepower);
        dest.writeString(this.firepowerUnit);
        dest.writeString(this.weight);
        dest.writeString(this.weightUnit);
        dest.writeString(this.cookingTemp);
        dest.writeString(this.cookingTime);
        dest.writeString(this.recipeConfig);
        dest.writeString(this.preAppointFirepower);
        dest.writeString(this.preAppointWeight);
        dest.writeString(this.preAppointCookingTemp);
        dest.writeString(this.preAppointCookingTime);
        dest.writeString(this.preAppointRecipeConfig);
        dest.writeByte(this.isNeedPreHeated ? (byte) 1 : (byte) 0);
        dest.writeString(this.preHeatTemp);
        dest.writeByte(this.isNormalCooking ? (byte) 1 : (byte) 0);
        dest.writeLong(this.normalCookingTime);
        dest.writeByte(this.isPreAppoint ? (byte) 1 : (byte) 0);
        dest.writeLong(this.preAppointTime);
        dest.writeByte(this.isFavorite ? (byte) 1 : (byte) 0);
        dest.writeLong(this.favoriteTime);
        dest.writeByte(this.hasSynchronizedFavorite ? (byte) 1 : (byte) 0);
        dest.writeLong(this.synchronizedFavoriteTime);
        dest.writeByte(this.hasSynchronizedPreAppoint ? (byte) 1 : (byte) 0);
        dest.writeLong(this.synchronizedPreAppointTime);
        dest.writeByte(this.hasSynchronizedCooking ? (byte) 1 : (byte) 0);
        dest.writeLong(this.synchronizedCookingTime);
    }

    public Long getId() {
        return this.id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public long getCreateTime() {
        return this.createTime;
    }

    public void setCreateTime(long createTime) {
        this.createTime = createTime;
    }

    public String getRecipeId() {
        return this.recipeId;
    }

    public void setRecipeId(String recipeId) {
        this.recipeId = recipeId;
    }

    public String getRecipeName() {
        return this.recipeName;
    }

    public void setRecipeName(String recipeName) {
        this.recipeName = recipeName;
    }

    public String getRecipeImgUrl() {
        return this.recipeImgUrl;
    }

    public void setRecipeImgUrl(String recipeImgUrl) {
        this.recipeImgUrl = recipeImgUrl;
    }

    public int getRecipeImgRes() {
        return this.recipeImgRes;
    }

    public void setRecipeImgRes(int recipeImgRes) {
        this.recipeImgRes = recipeImgRes;
    }

    public String getFirepower() {
        return this.firepower;
    }

    public void setFirepower(String firepower) {
        this.firepower = firepower;
    }

    public String getFirepowerUnit() {
        return this.firepowerUnit;
    }

    public void setFirepowerUnit(String firepowerUnit) {
        this.firepowerUnit = firepowerUnit;
    }

    public String getWeight() {
        return this.weight;
    }

    public void setWeight(String weight) {
        this.weight = weight;
    }

    public String getWeightUnit() {
        return this.weightUnit;
    }

    public void setWeightUnit(String weightUnit) {
        this.weightUnit = weightUnit;
    }

    public String getCookingTemp() {
        return this.cookingTemp;
    }

    public void setCookingTemp(String cookingTemp) {
        this.cookingTemp = cookingTemp;
    }

    public String getCookingTime() {
        return this.cookingTime;
    }

    public void setCookingTime(String cookingTime) {
        this.cookingTime = cookingTime;
    }

    public String getRecipeConfig() {
        return this.recipeConfig;
    }

    public void setRecipeConfig(String recipeConfig) {
        this.recipeConfig = recipeConfig;
    }

    public String getPreAppointFirepower() {
        return this.preAppointFirepower;
    }

    public void setPreAppointFirepower(String preAppointFirepower) {
        this.preAppointFirepower = preAppointFirepower;
    }

    public String getPreAppointWeight() {
        return this.preAppointWeight;
    }

    public void setPreAppointWeight(String preAppointWeight) {
        this.preAppointWeight = preAppointWeight;
    }

    public String getPreAppointCookingTemp() {
        return this.preAppointCookingTemp;
    }

    public void setPreAppointCookingTemp(String preAppointCookingTemp) {
        this.preAppointCookingTemp = preAppointCookingTemp;
    }

    public String getPreAppointCookingTime() {
        return this.preAppointCookingTime;
    }

    public void setPreAppointCookingTime(String preAppointCookingTime) {
        this.preAppointCookingTime = preAppointCookingTime;
    }

    public String getPreAppointRecipeConfig() {
        return this.preAppointRecipeConfig;
    }

    public void setPreAppointRecipeConfig(String preAppointRecipeConfig) {
        this.preAppointRecipeConfig = preAppointRecipeConfig;
    }

    public boolean getIsNeedPreHeated() {
        return this.isNeedPreHeated;
    }

    public void setIsNeedPreHeated(boolean isNeedPreHeated) {
        this.isNeedPreHeated = isNeedPreHeated;
    }

    public String getPreHeatTemp() {
        return this.preHeatTemp;
    }

    public void setPreHeatTemp(String preHeatTemp) {
        this.preHeatTemp = preHeatTemp;
    }

    public boolean getIsNormalCooking() {
        return this.isNormalCooking;
    }

    public void setIsNormalCooking(boolean isNormalCooking) {
        this.isNormalCooking = isNormalCooking;
    }

    public long getNormalCookingTime() {
        return this.normalCookingTime;
    }

    public void setNormalCookingTime(long normalCookingTime) {
        this.normalCookingTime = normalCookingTime;
    }

    public boolean getIsPreAppoint() {
        return this.isPreAppoint;
    }

    public void setIsPreAppoint(boolean isPreAppoint) {
        this.isPreAppoint = isPreAppoint;
    }

    public long getPreAppointTime() {
        return this.preAppointTime;
    }

    public void setPreAppointTime(long preAppointTime) {
        this.preAppointTime = preAppointTime;
    }

    public boolean getIsFavorite() {
        return this.isFavorite;
    }

    public void setIsFavorite(boolean isFavorite) {
        this.isFavorite = isFavorite;
    }

    public long getFavoriteTime() {
        return this.favoriteTime;
    }

    public void setFavoriteTime(long favoriteTime) {
        this.favoriteTime = favoriteTime;
    }

    public boolean getHasSynchronizedFavorite() {
        return this.hasSynchronizedFavorite;
    }

    public void setHasSynchronizedFavorite(boolean hasSynchronizedFavorite) {
        this.hasSynchronizedFavorite = hasSynchronizedFavorite;
    }

    public long getSynchronizedFavoriteTime() {
        return this.synchronizedFavoriteTime;
    }

    public void setSynchronizedFavoriteTime(long synchronizedFavoriteTime) {
        this.synchronizedFavoriteTime = synchronizedFavoriteTime;
    }

    public boolean getHasSynchronizedPreAppoint() {
        return this.hasSynchronizedPreAppoint;
    }

    public void setHasSynchronizedPreAppoint(boolean hasSynchronizedPreAppoint) {
        this.hasSynchronizedPreAppoint = hasSynchronizedPreAppoint;
    }

    public long getSynchronizedPreAppointTime() {
        return this.synchronizedPreAppointTime;
    }

    public void setSynchronizedPreAppointTime(long synchronizedPreAppointTime) {
        this.synchronizedPreAppointTime = synchronizedPreAppointTime;
    }

    public boolean getHasSynchronizedCooking() {
        return this.hasSynchronizedCooking;
    }

    public void setHasSynchronizedCooking(boolean hasSynchronizedCooking) {
        this.hasSynchronizedCooking = hasSynchronizedCooking;
    }

    public long getSynchronizedCookingTime() {
        return this.synchronizedCookingTime;
    }

    public void setSynchronizedCookingTime(long synchronizedCookingTime) {
        this.synchronizedCookingTime = synchronizedCookingTime;
    }

    public IotHistoryBean() {
    }

    protected IotHistoryBean(Parcel in) {
        this.id = (Long) in.readValue(Long.class.getClassLoader());
        this.createTime = in.readLong();
        this.recipeId = in.readString();
        this.recipeName = in.readString();
        this.recipeImgUrl = in.readString();
        this.recipeImgRes = in.readInt();
        this.firepower = in.readString();
        this.firepowerUnit = in.readString();
        this.weight = in.readString();
        this.weightUnit = in.readString();
        this.cookingTemp = in.readString();
        this.cookingTime = in.readString();
        this.recipeConfig = in.readString();
        this.preAppointFirepower = in.readString();
        this.preAppointWeight = in.readString();
        this.preAppointCookingTemp = in.readString();
        this.preAppointCookingTime = in.readString();
        this.preAppointRecipeConfig = in.readString();
        this.isNeedPreHeated = in.readByte() != 0;
        this.preHeatTemp = in.readString();
        this.isNormalCooking = in.readByte() != 0;
        this.normalCookingTime = in.readLong();
        this.isPreAppoint = in.readByte() != 0;
        this.preAppointTime = in.readLong();
        this.isFavorite = in.readByte() != 0;
        this.favoriteTime = in.readLong();
        this.hasSynchronizedFavorite = in.readByte() != 0;
        this.synchronizedFavoriteTime = in.readLong();
        this.hasSynchronizedPreAppoint = in.readByte() != 0;
        this.synchronizedPreAppointTime = in.readLong();
        this.hasSynchronizedCooking = in.readByte() != 0;
        this.synchronizedCookingTime = in.readLong();
    }

    @Generated(hash = 1780550136)
    public IotHistoryBean(Long id, long createTime, String recipeId, String recipeName,
            String recipeImgUrl, int recipeImgRes, String firepower, String firepowerUnit,
            String weight, String weightUnit, String cookingTemp, String cookingTime,
            String recipeConfig, String preAppointFirepower, String preAppointWeight,
            String preAppointCookingTemp, String preAppointCookingTime,
            String preAppointRecipeConfig, boolean isNeedPreHeated, String preHeatTemp,
            boolean isNormalCooking, long normalCookingTime, boolean isPreAppoint,
            long preAppointTime, boolean isFavorite, long favoriteTime,
            boolean hasSynchronizedFavorite, long synchronizedFavoriteTime,
            boolean hasSynchronizedPreAppoint, long synchronizedPreAppointTime,
            boolean hasSynchronizedCooking, long synchronizedCookingTime) {
        this.id = id;
        this.createTime = createTime;
        this.recipeId = recipeId;
        this.recipeName = recipeName;
        this.recipeImgUrl = recipeImgUrl;
        this.recipeImgRes = recipeImgRes;
        this.firepower = firepower;
        this.firepowerUnit = firepowerUnit;
        this.weight = weight;
        this.weightUnit = weightUnit;
        this.cookingTemp = cookingTemp;
        this.cookingTime = cookingTime;
        this.recipeConfig = recipeConfig;
        this.preAppointFirepower = preAppointFirepower;
        this.preAppointWeight = preAppointWeight;
        this.preAppointCookingTemp = preAppointCookingTemp;
        this.preAppointCookingTime = preAppointCookingTime;
        this.preAppointRecipeConfig = preAppointRecipeConfig;
        this.isNeedPreHeated = isNeedPreHeated;
        this.preHeatTemp = preHeatTemp;
        this.isNormalCooking = isNormalCooking;
        this.normalCookingTime = normalCookingTime;
        this.isPreAppoint = isPreAppoint;
        this.preAppointTime = preAppointTime;
        this.isFavorite = isFavorite;
        this.favoriteTime = favoriteTime;
        this.hasSynchronizedFavorite = hasSynchronizedFavorite;
        this.synchronizedFavoriteTime = synchronizedFavoriteTime;
        this.hasSynchronizedPreAppoint = hasSynchronizedPreAppoint;
        this.synchronizedPreAppointTime = synchronizedPreAppointTime;
        this.hasSynchronizedCooking = hasSynchronizedCooking;
        this.synchronizedCookingTime = synchronizedCookingTime;
    }

    public static final Creator<IotHistoryBean> CREATOR = new Creator<IotHistoryBean>() {
        @Override
        public IotHistoryBean createFromParcel(Parcel source) {
            return new IotHistoryBean(source);
        }

        @Override
        public IotHistoryBean[] newArray(int size) {
            return new IotHistoryBean[size];
        }
    };
}

```

**以下是正确查询语句：**
```java
/**
 * 获取指定条数的收藏历史记录
 * 需要做去重处理
 *
 * @return
 */
public synchronized static List<IotHistoryBean> getFavoriteList(int count) {
    String queryString = "SELECT DISTINCT " + IotHistoryBeanDao.Properties.RecipeId.columnName
            + "," + IotHistoryBeanDao.Properties.RecipeName.columnName
            + "," + IotHistoryBeanDao.Properties.RecipeImgUrl.columnName
            + "," + IotHistoryBeanDao.Properties.RecipeImgRes.columnName
            + "," + IotHistoryBeanDao.Properties.FavoriteTime.columnName
            + " FROM " + IotHistoryBeanDao.TABLENAME
            + " WHERE " + IotHistoryBeanDao.Properties.IsFavorite.columnName + " = \'1\'"
            + " ORDER BY " + IotHistoryBeanDao.Properties.FavoriteTime.columnName + " DESC"
            + " LIMIT " + count;

    ArrayList<IotHistoryBean> result = new ArrayList<>();
    Cursor c = DbManager.getDaoSession(App.getContext())
            .getDatabase()
            .rawQuery(queryString, null);
    try {
        if (c != null && c.moveToFirst() && c.getCount() > 0) {
            do {
                IotHistoryBean iotHistoryBean = new IotHistoryBean();
                iotHistoryBean.setRecipeId(c.getString(c.getColumnIndex(IotHistoryBeanDao.Properties.RecipeId.columnName)));
                iotHistoryBean.setRecipeName(c.getString(c.getColumnIndex(IotHistoryBeanDao.Properties.RecipeName.columnName)));
                iotHistoryBean.setRecipeImgUrl(c.getString(c.getColumnIndex(IotHistoryBeanDao.Properties.RecipeImgUrl.columnName)));
                iotHistoryBean.setRecipeImgRes(c.getInt(c.getColumnIndex(IotHistoryBeanDao.Properties.RecipeImgRes.columnName)));
                iotHistoryBean.setFavoriteTime(c.getLong(c.getColumnIndex(IotHistoryBeanDao.Properties.FavoriteTime.columnName)));
                result.add(iotHistoryBean);
            } while (c.moveToNext());
        }
    } finally {
        if (c != null) {
            c.close();
        }
    }
    return result;
}
```


问题出现在WHERE语句，由于IsFavorite字段是被定义为布尔类型，出现了以下几种情况：

**1.** android.database.sqlite.SQLiteException: no such column: TRUE (code 1): , while compiling: SELECT DISTINCT RECIPE_ID,RECIPE_NAME,RECIPE_IMG_URL,RECIPE_IMG_RES,FAVORITE_TIME FROM IOT_HISTORY_BEAN WHERE IS_FAVORITE = TRUE ORDER BY FAVORITE_TIME DESC LIMIT 20

```java
String queryString = "SELECT DISTINCT " + IotHistoryBeanDao.Properties.RecipeId.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeName.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeImgUrl.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeImgRes.columnName
        + "," + IotHistoryBeanDao.Properties.FavoriteTime.columnName
        + " FROM " + IotHistoryBeanDao.TABLENAME
        + " WHERE " + IotHistoryBeanDao.Properties.IsFavorite.columnName + " = TRUE"
        + " ORDER BY " + IotHistoryBeanDao.Properties.FavoriteTime.columnName + " DESC"
        + " LIMIT " + count;

ArrayList<IotHistoryBean> result = new ArrayList<>();
Cursor c = DbManager.getDaoSession(App.getContext())
        .getDatabase()
        .rawQuery(queryString, null);
```

**2.** 以下几种没发现报错，但获取不到想要的数据

第一种：
```java
String queryString = "SELECT DISTINCT " + IotHistoryBeanDao.Properties.RecipeId.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeName.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeImgUrl.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeImgRes.columnName
        + "," + IotHistoryBeanDao.Properties.FavoriteTime.columnName
        + " FROM " + IotHistoryBeanDao.TABLENAME
        + " WHERE " + IotHistoryBeanDao.Properties.IsFavorite.columnName + " = 1"
        + " ORDER BY " + IotHistoryBeanDao.Properties.FavoriteTime.columnName + " DESC"
        + " LIMIT " + count;

ArrayList<IotHistoryBean> result = new ArrayList<>();
Cursor c = DbManager.getDaoSession(App.getContext())
        .getDatabase()
        .rawQuery(queryString, null);
```
第二种：
```java
String queryString = "SELECT DISTINCT " + IotHistoryBeanDao.Properties.RecipeId.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeName.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeImgUrl.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeImgRes.columnName
        + "," + IotHistoryBeanDao.Properties.FavoriteTime.columnName
        + " FROM " + IotHistoryBeanDao.TABLENAME
        + " WHERE " + IotHistoryBeanDao.Properties.IsFavorite.columnName + " = ?"
        + " ORDER BY " + IotHistoryBeanDao.Properties.FavoriteTime.columnName + " DESC"
        + " LIMIT " + count;

ArrayList<IotHistoryBean> result = new ArrayList<>();
Cursor c = DbManager.getDaoSession(App.getContext())
        .getDatabase()
        .rawQuery(queryString, new String[]{"true"});
```
第三种：
```java
String queryString = "SELECT DISTINCT " + IotHistoryBeanDao.Properties.RecipeId.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeName.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeImgUrl.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeImgRes.columnName
        + "," + IotHistoryBeanDao.Properties.FavoriteTime.columnName
        + " FROM " + IotHistoryBeanDao.TABLENAME
        + " WHERE " + IotHistoryBeanDao.Properties.IsFavorite.columnName + " = ?"
        + " ORDER BY " + IotHistoryBeanDao.Properties.FavoriteTime.columnName + " DESC"
        + " LIMIT " + count;

ArrayList<IotHistoryBean> result = new ArrayList<>();
Cursor c = DbManager.getDaoSession(App.getContext())
        .getDatabase()
        .rawQuery(queryString, new String[]{"1"});
```
第四种：
```java
String queryString = "SELECT DISTINCT " + IotHistoryBeanDao.Properties.RecipeId.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeName.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeImgUrl.columnName
        + "," + IotHistoryBeanDao.Properties.RecipeImgRes.columnName
        + "," + IotHistoryBeanDao.Properties.FavoriteTime.columnName
        + " FROM " + IotHistoryBeanDao.TABLENAME
        + " WHERE " + IotHistoryBeanDao.Properties.IsFavorite.columnName + " = \'TRUE\'"
        + " ORDER BY " + IotHistoryBeanDao.Properties.FavoriteTime.columnName + " DESC"
        + " LIMIT " + count;

ArrayList<IotHistoryBean> result = new ArrayList<>();
Cursor c = DbManager.getDaoSession(App.getContext())
        .getDatabase()
        .rawQuery(queryString, null);
```