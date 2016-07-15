---
layout: post
title:  "Had a play with Core Motion"
date:   2016-07-15
excerpt: "Fun and anoying."
project: true

tag:
- CoreMotion

comments: false
---

# Had a play with Core Motion

Pedometer counting function is pretty popular in fitness app generally. Here is the way I achieved this function in my App.

***To get pedometer of last 7 days***

```
if CMPedometer.isStepCountingAvailable() {
    let serialQueue : dispatch_queue_t  = dispatch_queue_create("com.pedometer.MyQueue", nil)
    let formatter = NSDateFormatter()
    formatter.dateFormat = "d MMM"
    dispatch_sync(serialQueue, { () -> Void in
        for day in 0...6 {
            let startDate = NSDate(timeIntervalSinceNow: Double(-7 + day) * 86400)
            let endDate = NSDate(timeIntervalSinceNow: Double(-7 + day + 1) * 86400)
            let dateString = formatter.stringFromDate(endDate)
            self.pedoMeter.queryPedometerDataFromDate(startDate, toDate: endDate) { (CMData: CMPedometerData?, errors:NSError?) -> Void in
                guard let data = CMData else { return }
                cell.numberSteps.text = "\(data.numberOfSteps)"
                self.days.append(dateString)
                self.result.append(data.numberOfSteps.integerValue)
                if(self.days.count == 7){
                    dispatch_sync(dispatch_get_main_queue(), { () -> Void in
                        let view = self.result.lineGraph().view(cell.graphicView.bounds).lineGraphConfiguration({ LineGraphViewConfig(lineColor: GWMColorRed, contentInsets: UIEdgeInsets(top: 32.0, left: 32.0, bottom: 32.0, right: 32.0)) })
                        view.autoresizingMask = [.FlexibleWidth, .FlexibleHeight]
                        cell.graphicView.addSubview(view)
                        cell.graphicView.layer.borderWidth = 1
                        cell.graphicView.layer.borderColor = GWMColorRed.CGColor
                    })
                }
                
            }
        }
    })
}
```
I read through the document of Core Motion about `queryPedometerDataFromDate` method. I dont really understand why this pedometer has to be getting from the call-back handler rather than just value return straightaway. Well I guess, it may be Core Motion function is running on the coprocessor, as steps counting function only availble on A7 processor above. Anyway, since it use call-back handler to give the pedometers and also the diagram need to get the pedometer first before draw the diagram, so I need to get all the pedometers from last 7 days first, then draw the diagram.
The reason I use dispatch_sync, not dispatch_async is that dispatch_sync will submit the blocks and wait until block is completed. So I open a queue to hold and loop through 7 times to get the pedometer of last 7days. Once it down and we collected all the datas then we draw the diagram. The framework I used for the diagram is a very light weight diagram framework called "[Graphs](https://github.com/recruit-mtl/Graphs)". Maybe it's bit way too light, some of feature they should have in a basic graph/charts but they didnt included. I will see whats going on with their updates and may change to other framework for the charts.
