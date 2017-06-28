# Working with date and time
* Events in the past save as timestamps (in UTC)
* Events scheduled in the future: 

> Instead of saving the time in UTC along with the time zone, 
> developers can save what the user expects us to save: the wall time. 
> Ie. what the clock on the wall will say. In the example that would be 10:00. 
> And we also save the timezone (Santiago/Chile). This way we can convert back to UTC or any other timezone.

(~ http://www.creativedeletion.com/2015/03/19/persisting_future_datetimes.html)
