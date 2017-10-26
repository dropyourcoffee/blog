---
layout: post
title:  "AST System Clock Implementation (nRF52 example)"
date:   2017-07-18 12:43:53 +0900
categories: Embedded/nRF52
---


Not a working example, just excerpt from code.
<br><br>

ast_timer.h
{% highlight c %}
#define IS_LEAP_YEAR(a)	((a % 400) == 0 || ((a % 4) == 0 && (a % 100)))

#pragma anon_unions

struct ast_calv {
  /** Seconds in the range 0 to 59. */
  uint32_t sec   : 6;
  /** Minutes in the range range 0 to 59. */
  uint32_t min   : 6;
  /** Hours in the range 0 to 23. */
  uint32_t hour  : 5;
  /** Day in the range 1 to 31. */
  uint32_t day   : 5;
  /** Month in the range 1 to 12. */
  uint32_t month : 4;
  /** Year in the range 0 to 63. */
  uint32_t year  : 6;
};

typedef struct  {
  union {
    uint32_t field;
    struct ast_calv FIELD;
  };
} ast_calendar_t;

static void sys_tick_cb(void * p_context);

{% endhighlight %}

<br>

ast_timer.c
{% highlight c %}
static void sys_tick_cb(void * p_context)
{
  if( ++Time.FIELD.sec % 60 == 0 ){
    Time.FIELD.sec = 0;
    Time.FIELD.min++;

    if(Time.FIELD.min % 60 == 0 ){
      Time.FIELD.min = 0;
      Time.FIELD.hour++;

      if(Time.FIELD.hour % 24 == 0 ){
        Time.FIELD.hour = 0;
        Time.FIELD.day++;

          switch(Time.FIELD.month){
            case 1:
            case 3:
            case 5:
            case 7:
            case 8:
            case 10:
            case 12:
              if(Time.FIELD.day % 32 == 0){
                Time.FIELD.day = 1;
                Time.FIELD.month++;
                }
                break;

            case 4:
            case 6:
            case 9:
            case 11:
              if(Time.FIELD.day % 31 == 0){
                Time.FIELD.day = 1;
                Time.FIELD.month++;
                }
                break;

            case 2:
               if( IS_LEAP_YEAR(Time.FIELD.year) ){
                 if(Time.FIELD.day > 29){
                   Time.FIELD.day = 1;
                   Time.FIELD.month++;
                   }
               }else{
                 if(Time.FIELD.day > 28){
                   Time.FIELD.day = 1;
                   Time.FIELD.month++;
                 }
               }
               break;
          }

          if( Time.FIELD.month > 12 ){
            Time.FIELD.month = 1;
            Time.FIELD.year++;
          }

      }// end if(Time.FIELD.hour % 24 == 0 )
    }
  }
}


{% endhighlight %}


<br>

### nRF5x Example

{% highlight c %}

// ticks per second.
#define SYS_TIME_TICK_INTERVAL      APP_TIMER_TICKS(1000, APP_TIMER_PRESCALER)

APP_TIMER_DEF(m_sys_timer_id);

void bt_init(void)
{
  uint32_t err_code;

  // Initialize timer module.
  APP_TIMER_INIT(APP_TIMER_PRESCALER, APP_TIMER_OP_QUEUE_SIZE, false);
  err_code = app_timer_create(&m_sys_timer_id, APP_TIMER_MODE_REPEATED, sys_tick_cb );
  APP_ERROR_CHECK(err_code);

  // Start Timer
  err_code = app_timer_start(m_sys_timer_id, SYS_TIME_TICK_INTERVAL, NULL);
  APP_ERROR_CHECK(err_code);
}
// Time initialization 2016-01-01T00:00:00
volatile ast_calendar_t Time = {
  .FIELD.year   = 16,
  .FIELD.month  = 1,
  .FIELD.day    = 1,
  .FIELD.hour   = 0,
  .FIELD.min    = 0,
  .FIELD.sec    = 0
};


{% endhighlight %}