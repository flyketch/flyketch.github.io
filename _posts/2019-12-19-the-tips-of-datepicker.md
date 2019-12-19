## element ui datepicker 时间控制

```javascript
<el-date-picker
  style="width:195px"
  value-format="yyyy-MM-dd"
  v-model="form.start_date"
  type="date"
  :picker-options="pickerOptions"
  placeholder="选择日期">
</el-date-picker>

data() {
  return {
    pickerOptions1: {
      disabledDate(time) {
        return time.getTime() < Date.now() - 8.64e7;
      },

      disabledDate: (time) => {
        if (this.curDate) {
          const one = 30 * 24 * 3600 * 1000
          const minTime = this.curDate - one
          const maxTime = this.curDate + one
          return time.getTime() < minTime || time.getTime() > maxTime
        }
      }
    }
  }
}
```