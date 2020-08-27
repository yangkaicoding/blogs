#### 前言

- 自动生成编号
```java
    /**
     * 自动生成编号
     * 自动生成规则：4位年+2位月+2位日+4位流水号
     *
     * @return String
     */
    public static Long generateNumber() {
        StringBuilder str = new StringBuilder();
        String date = new SimpleDateFormat("yyyyMMdd").format(new Date());
        str.append(date);
        Random random = new Random();
        for (int i = 0; i < 4; i++) {
            str.append(random.nextInt(10));
        }
        return Long.valueOf(str.toString);
    }
```