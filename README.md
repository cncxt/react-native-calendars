**备注** <br>
  翻译为中文 方便查看

---


# React Native Calendars ✨ 🗓️ 📆
[![Version](https://img.shields.io/npm/v/react-native-calendars.svg)](https://www.npmjs.com/package/react-native-calendars)
[![Build Status](https://travis-ci.org/wix/react-native-calendars.svg?branch=master)](https://travis-ci.org/wix/react-native-calendars)

本插件涵盖了各种各样的自定义的React Native 组件

本开发包同时兼容 **Android** and **iOS** .

##小试牛刀

运行下面的命令，你可以查看我们提供的示例:

```
$ git clone git@github.com:wix/react-native-calendars.git
$ npm install
$ react-native run-ios
```

You can check example screens source code in [example module screens](https://github.com/wix-private/wix-react-native-calendar/tree/master/example/src/screens)

This project is compatible with Expo/CRNA (without ejecting), and the examples have been [published on Expo](https://expo.io/@community/react-native-calendars-example)

## 安装

```
$ npm install --save react-native-calendars
```

本插件是使用JavaScript来实现的，所以并不需要链接原生的模块。

## 用法

`import {`[Calendar](#calendar), [CalendarList](#calendarlist), [Agenda](#agenda)`} from 'react-native-calendars';`

本组件的所有参数都是可选的. 默认显示的是当前本地时间的月份.

Event handler callbacks are called with `calendar objects` like this:

```javasctipt
{
  day: 1,     // day of month (1-31)
  month: 1,   // month of year (1-12)
  year: 2017, // year
  timestamp,   // UTC timestamp representing 00:00 AM of this date
  dateString: '2016-05-13' // date formatted as 'YYYY-MM-DD' string
}
```

参数中的日期类型要求可以是"YYYY-MM-DD"形式的日期字符串，JavaScript日期对象，calendar对象，或者UTC时间戳

你可以向LocaleConfig对象中添加本地标识来实现日历的本地化

```javascript
import {LocaleConfig} from 'react-native-calendars';

LocaleConfig.locales['fr'] = {
  monthNames: ['Janvier','Février','Mars','Avril','Mai','Juin','Juillet','Août','Septembre','Octobre','Novembre','Décembre'],
  monthNamesShort: ['Janv.','Févr.','Mars','Avril','Mai','Juin','Juil.','Août','Sept.','Oct.','Nov.','Déc.'],
  dayNames: ['Dimanche','Lundi','Mardi','Mercredi','Jeudi','Vendredi','Samedi'],
  dayNamesShort: ['Dim.','Lun.','Mar.','Mer.','Jeu.','Ven.','Sam.'],
  today: 'Aujourd\'hui'
};
LocaleConfig.defaultLocale = 'fr';
```

### 日历

<kbd>
  <img src="https://github.com/wix-private/wix-react-native-calendar/blob/master/demo/calendar.gif?raw=true">
</kbd>

#### Basic parameters

```javascript
<Calendar
  // 初始化所显示的月份，默认是当前月份
  current={'2012-03-01'}
  // 设置可选日期的最早日期，比这个日期更早的日期会用灰色显示。默认是undefined.
  minDate={'2012-05-10'}
  // 设置可选日期的最晚日期，比这个日期更晚的日期会用灰色显示，默认是undefined.
  maxDate={'2012-05-30'}
  // 点击日期的处理函数，当你手指按下日期中的某一天会触发这个函数。默认是undefined
  onDayPress={(day) => {console.log('selected day', day)}}
  // 长按日期的处理函数，当你手指长时间按住日期中的某一天会触发这个函数。默认是undefined
  onDayLongPress={(day) => {console.log('selected day', day)}}
  // 设置日历标题中月份的格式，格式参考：http://arshaw.com/xdate/#Formatting
  monthFormat={'yyyy MM'}
  // 当日历中的月份改变的时候会触发这个函数，默认为undefined
  onMonthChange={(month) => {console.log('month changed', month)}}
  // 是否隐藏选择月份的箭头，默认为false不隐藏
  hideArrows={true}
  // 使用自定义的图标来替换默认的箭头（方向可以是‘left’ 或者 ‘right’）
  renderArrow={(direction) => (<Arrow />)}
  // 不在当前月份中显示其他月份的日期，默认为false显示
  hideExtraDays={true}
  // 如果 hideArrows=false 并且 hideExtraDays=false 当点击外部的灰色日期的时候不跳转月份
  // 在日历面板中是否显示其他月份的日期，默认为false不显示
  disableMonthChange={true}
  // 如果 firstDay=1 每周从周一开始.需要注意的是dayNames和hayNamesShort仍然以周日为开端
  firstDay={1}
  // 是否隐藏日期的名字，默认为false不隐藏
  hideDayNames={true}
  // 是否在左侧显示周几，默认为false不显示
  showWeekNumbers={true}
  // 当点击左侧箭头图标的时候会执行这个函数。它还有一个回调函数，可以前滚一个月
  onPressArrowLeft={substractMonth => substractMonth()}
  // 当点击右侧箭头图标的时候会执行这个函数。它还有一个回调函数，可以后滚一个月
  onPressArrowRight={addMonth => addMonth()}
/>
```

#### 日期的标记

**!注意!** 不要更改参数 `markedDates`. 如果你更改了这个对象 但是没有更改对其的引用的话，日历更新就不会触发标记效果。
以点来标记

<kbd>
  <img height=50 src="https://github.com/wix-private/wix-react-native-calendar/blob/master/demo/marking1.png?raw=true">
</kbd>

```javascript
<Calendar
  //需要标记的日期的集合 Default = {}
  markedDates={{
    '2012-05-16': {selected: true, marked: true, selectedColor: 'blue'},
    '2012-05-17': {marked: true},
    '2012-05-18': {marked: true, dotColor: 'red', activeOpacity: 0},
    '2012-05-19': {disabled: true, disableTouchEvent: true}
  }}
/>
```

你可以为单独的日期定义一个颜色.

以多个点来标记日期

<kbd>
 <img height=50 src="https://github.com/wix-private/wix-react-native-calendar/blob/master/demo/marking4.png?raw=true">
</kbd>

Use markingType = 'multi-dot' if you want to display more than one dot. Both the Calendar and CalendarList control support multiple dots by using 'dots' array in markedDates. The property 'color' is mandatory while 'key' and 'selectedColor' are optional. If key is omitted then the array index is used as key. If selectedColor is omitted then 'color' will be used for selected dates.
```javascript
const vacation = {key:'vacation', color: 'red', selectedDotColor: 'blue'};
const massage = {key:'massage', color: 'blue', selectedDotColor: 'blue'};
const workout = {key:'workout', color: 'green'};

<Calendar
  markedDates={{
    '2017-10-25': {dots: [vacation, massage, workout], selected: true, selectedColor: 'red'},
    '2017-10-26': {dots: [massage, workout], disabled: true}
  }}
  markingType={'multi-dot'}
/>
```


Period marking

<kbd>
  <img height=50 src="https://github.com/wix-private/wix-react-native-calendar/blob/master/demo/marking2.png?raw=true">
</kbd>

<kbd>
  <img height=50 src="https://github.com/wix-private/wix-react-native-calendar/blob/master/demo/marking3.png?raw=true">
</kbd>

```javascript
<Calendar
  // Collection of dates that have to be colored in a special way. Default = {}
  markedDates={{
    '2012-05-20': {textColor: 'green'},
    '2012-05-22': {startingDay: true, color: 'green'},
    '2012-05-23': {selected: true, endingDay: true, color: 'green', textColor: 'gray'},
    '2012-05-04': {disabled: true, startingDay: true, color: 'green', endingDay: true}
  }}
  // Date marking style [simple/period/multi-dot/custom]. Default = 'simple'
  markingType={'period'}
/>
```

Multi-period marking

<kbd>
  <img height=50 src="https://github.com/wix-private/wix-react-native-calendar/blob/master/demo/marking6.png?raw=true">
</kbd>

CAUTION: This marking is only fully supported by the `<Calendar />` component because it expands its height. Usage with `<CalendarList />` might lead to overflow issues.

```javascript
<Calendar
  markedDates={{
    '2017-12-14': {
      periods: [
        { startingDay: false, endingDay: true, color: '#5f9ea0' },
        { startingDay: false, endingDay: true, color: '#ffa500' },
        { startingDay: true, endingDay: false, color: '#f0e68c' },
      ]
    },
    '2017-12-15': {
      periods: [
        { startingDay: true, endingDay: false, color: '#ffa500' },
        { color: 'transparent' },
        { startingDay: false, endingDay: false, color: '#f0e68c' },
      ]
    },
  }}
  // Date marking style [simple/period/multi-dot/custom]. Default = 'simple'
  markingType='multi-period'
/>
```

Custom marking allows you to customize each marker with custom styles.

<kbd>
  <img height=50 src="https://github.com/wix-private/wix-react-native-calendar/blob/master/demo/custom.png?raw=true">
</kbd>

```javascript
<Calendar
  // Date marking style [simple/period/multi-dot/single]. Default = 'simple'
  markingType={'custom'}
  markedDates={{
    '2018-03-28': {
      customStyles: {
        container: {
          backgroundColor: 'green'
        },
        text: {
          color: 'black',
          fontWeight: 'bold'
        },
      },
    },
    '2018-03-29': {
      customStyles: {
        container: {
          backgroundColor: 'white',
          elevation: 2
        },
        text: {
          color: 'blue'
        },
      }
    }
  }}
/>
```

Keep in mind that different marking types are not compatible. You can use just one marking style for calendar.

#### Displaying data loading indicator

<kbd>
  <img height=50 src="https://github.com/wix-private/wix-react-native-calendar/blob/master/demo/loader.png?raw=true">
</kbd>

The loading indicator next to month name will be displayed if `<Calendar />` has `displayLoadingIndicator` property and `markedDates` collection does not have a value for every day of the month in question. When you load data for days, just set `[]` or special marking value to all days in `markedDates` collection.

#### Customizing look & feel

```javascript
<Calendar
  // Specify style for calendar container element. Default = {}
  style={{
    borderWidth: 1,
    borderColor: 'gray',
    height: 350
  }}
  // Specify theme properties to override specific styles for calendar parts. Default = {}
  theme={{
    backgroundColor: '#ffffff',
    calendarBackground: '#ffffff',
    textSectionTitleColor: '#b6c1cd',
    selectedDayBackgroundColor: '#00adf5',
    selectedDayTextColor: '#ffffff',
    todayTextColor: '#00adf5',
    dayTextColor: '#2d4150',
    textDisabledColor: '#d9e1e8',
    dotColor: '#00adf5',
    selectedDotColor: '#ffffff',
    arrowColor: 'orange',
    monthTextColor: 'blue',
    indicatorColor: 'blue',
    textDayFontFamily: 'monospace',
    textMonthFontFamily: 'monospace',
    textDayHeaderFontFamily: 'monospace',
    textDayFontWeight: '300',
    textMonthFontWeight: 'bold',
    textDayHeaderFontWeight: '300',
    textDayFontSize: 16,
    textMonthFontSize: 16,
    textDayHeaderFontSize: 16
  }}
/>
```

#### Advanced styling

If you want to have complete control over calendar styles you can do it by overriding default style.js files. For example, if you want to override calendar header style first you have to find stylesheet id for this file:

https://github.com/wix/react-native-calendars/blob/master/src/calendar/header/style.js#L4

In this case it is 'stylesheet.calendar.header'. Next you can add overriding stylesheet to your theme with this id.

https://github.com/wix/react-native-calendars/blob/master/example/src/screens/calendars.js#L56

```javascript
theme={{
  arrowColor: 'white',
  'stylesheet.calendar.header': {
    week: {
      marginTop: 5,
      flexDirection: 'row',
      justifyContent: 'space-between'
    }
  }
}}
```

**Disclaimer**: issues that arise because something breaks after using stylesheet override will not be supported. Use this option at your own risk.

#### Overriding day component

If you need custom functionality not supported by current day component implementations you can pass your own custom day
component to the calendar.

```javascript
<Calendar
  style={[styles.calendar, {height: 300}]}
  dayComponent={({date, state}) => {
    return (<View style={{flex: 1}}><Text style={{textAlign: 'center', color: state === 'disabled' ? 'gray' : 'black'}}>{date.day}</Text></View>);
  }}
/>
```

The dayComponent prop has to receive a RN component or function that receive props. The day component will receive such props:

* state - disabled if the day should be disabled (this is decided by base calendar component)
* marking - markedDates value for this day
* date - the date object representing this day

**Tip:** Don't forget to implement shouldComponentUpdate for your custom day component to make calendar perform better

If you implement an awesome day component please make a PR so that other people could use it :)

### CalendarList

<kbd>
  <img src="https://github.com/wix-private/wix-react-native-calendar/blob/master/demo/calendar-list.gif?raw=true">
</kbd>

`<CalendarList />` is scrollable semi-infinite calendar composed of `<Calendar />` components. Currently it is possible to scroll 4 years back and 4 years to the future. All paramters that are available for `<Calendar />` are also available for this component. There are also some additional params that can be used:

```javascript
<CalendarList
  // Callback which gets executed when visible months change in scroll view. Default = undefined
  onVisibleMonthsChange={(months) => {console.log('now these months are visible', months);}}
  // Max amount of months allowed to scroll to the past. Default = 50
  pastScrollRange={50}
  // Max amount of months allowed to scroll to the future. Default = 50
  futureScrollRange={50}
  // Enable or disable scrolling of calendar list
  scrollEnabled={true}
  // Enable or disable vertical scroll indicator. Default = false
  showScrollIndicator={true}
  ...calendarParams
/>
```

#### Horizontal CalendarList

<kbd>
  <img src="https://github.com/wix-private/wix-react-native-calendar/blob/master/demo/horizontal-calendar-list.gif?raw=true">
</kbd>

You can also make the `CalendarList` scroll horizontally. To do that you need to pass specific props to the `CalendarList`:

```javascript
<CalendarList
  // Enable horizontal scrolling, default = false
  horizontal={true}
  // Enable paging on horizontal, default = false
  pagingEnabled={true}
  // Set custom calendarWidth.
  calendarWidth={320}
  ...calendarListParams
  ...calendarParams
/>
```

### Agenda
<kbd>
  <img src="https://github.com/wix-private/wix-react-native-calendar/blob/master/demo/agenda.gif?raw=true">
</kbd>

An advanced agenda component that can display interactive listings for calendar day items.

```javascript
<Agenda
  // the list of items that have to be displayed in agenda. If you want to render item as empty date
  // the value of date key kas to be an empty array []. If there exists no value for date key it is
  // considered that the date in question is not yet loaded
  items={{
    '2012-05-22': [{text: 'item 1 - any js object'}],
    '2012-05-23': [{text: 'item 2 - any js object'}],
    '2012-05-24': [],
    '2012-05-25': [{text: 'item 3 - any js object'},{text: 'any js object'}]
  }}
  // callback that gets called when items for a certain month should be loaded (month became visible)
  loadItemsForMonth={(month) => {console.log('trigger items loading')}}
  // callback that fires when the calendar is opened or closed
  onCalendarToggled={(calendarOpened) => {console.log(calendarOpened)}}
  // callback that gets called on day press
  onDayPress={(day)=>{console.log('day pressed')}}
  // callback that gets called when day changes while scrolling agenda list
  onDayChange={(day)=>{console.log('day changed')}}
  // initially selected day
  selected={'2012-05-16'}
  // Minimum date that can be selected, dates before minDate will be grayed out. Default = undefined
  minDate={'2012-05-10'}
  // Maximum date that can be selected, dates after maxDate will be grayed out. Default = undefined
  maxDate={'2012-05-30'}
  // Max amount of months allowed to scroll to the past. Default = 50
  pastScrollRange={50}
  // Max amount of months allowed to scroll to the future. Default = 50
  futureScrollRange={50}
  // specify how each item should be rendered in agenda
  renderItem={(item, firstItemInDay) => {return (<View />);}}
  // specify how each date should be rendered. day can be undefined if the item is not first in that day.
  renderDay={(day, item) => {return (<View />);}}
  // specify how empty date content with no items should be rendered
  renderEmptyDate={() => {return (<View />);}}
  // specify how agenda knob should look like
  renderKnob={() => {return (<View />);}}
  // specify what should be rendered instead of ActivityIndicator
  renderEmptyData = {() => {return (<View />);}}
  // specify your item comparison function for increased performance
  rowHasChanged={(r1, r2) => {return r1.text !== r2.text}}
  // Hide knob button. Default = false
  hideKnob={true}
  // By default, agenda dates are marked if they have at least one item, but you can override this if needed
  markedDates={{
    '2012-05-16': {selected: true, marked: true},
    '2012-05-17': {marked: true},
    '2012-05-18': {disabled: true}
  }}
  // If provided, a standard RefreshControl will be added for "Pull to Refresh" functionality. Make sure to also set the refreshing prop correctly.
  onRefresh={() => console.log('refreshing...')}
  // Set this true while waiting for new data from a refresh
  refreshing={false}
  // Add a custom RefreshControl component, used to provide pull-to-refresh functionality for the ScrollView.
  refreshControl={null}
  // agenda theme
  theme={{
    ...calendarTheme,
    agendaDayTextColor: 'yellow',
    agendaDayNumColor: 'green',
    agendaTodayColor: 'red',
    agendaKnobColor: 'blue'
  }}
  // agenda container style
  style={{}}
/>
```

## Authors

* [Tautvilas Mecinskas](https://github.com/tautvilas/) - Initial code - [@tautvilas](https://twitter.com/TautviIas)
* Katrin Zotchev - Initial design - [@katrin_zot](https://twitter.com/katrin_zot)

See also the list of [contributors](https://github.com/wix/react-native-calendar-components/contributors) who participated in this project.

## Contributing

Pull requests are welcome. `npm run test` and `npm run lint` before push.
