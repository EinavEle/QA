Failure atomicity means we want our failures's effect to be minimal.
So if something fails we can still continue to operate.
Keeping the object's state valid is our main goal so if we can manage it while errors are thrown it is optimal.

Parameter validation, which we have discussed earlier, is a great option.
It allows us to check the validity of the parameters affecting the process and make sure we don't change an object's state before we know everything is valid and expected to work correctly.
```
  public void setStartDate(Date date){
      if(date.before(MIN_DATE)){
          throw new IllegalArgumentException(String.format("Date must be after: %s but was: %s", MIN_DATE, date));
      }
      this.startDate = date;
  }
```
This way we have a valid object even if an exception was thrown.

Another way to achieve failure atomicity is to work on a cloned object and only copy it back to the original when the process is done without errors.

Keep in mind that failure atomicity can be costly and not always worth it.
Make sure that it is worth the extra code and performance before you decide to implement it.

