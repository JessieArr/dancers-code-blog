---
title: "Navigating the Facebook App Review Process"
date: "2019-02-26"
---

Attempting to get a Facebook app approved for a new permission can be a very frustrating process. Despite my best efforts, I recently found myself waiting for 15 days and had to reapply no fewer than 6 times in order to get permission to link to users' profiles from my Facebook app.

I found Facebook's documentation - while voluminous - to be very disorganized which made it difficult to find exactly what I needed to move forward. Furthermore, the review process itself feels very opaque and bureaucratic, which was frustrating. But now that I've survived the process, and finally had my application approved, I wanted to offer some guidance to future developers attempting to get their App Reviewed.

## Know What You Need

First and foremost, any permissions your app uses must be granted to your app when the user logs in initially. For a full list of permissions you can request during login, check out the [Facebook Login Permissions documentation](https://developers.facebook.com/docs/facebook-login/permissions).

![chrome_2019-02-25_22-18-01](images/chrome_2019-02-25_22-18-01.jpg)

The documentation gives guidance about valid use cases for each permission - so read up on the permission you hope to use and make sure your use case is allowed by Facebook before applying for App Review.

Also note that [some permissions](https://developers.facebook.com/docs/facebook-login/changelog?hc_location=ufi#2018-07-02) require [Business Verification](https://developers.facebook.com/docs/apps/review/#business-verification) - this will not be available to Individual app developers and will require a Business profile to be associated with your app account, and you will have to sign a contract with Facebook attesting that you will not abuse your app permissions, and will comply with their information privacy rules etc.

## Where to Ask for Help

Facebook has an official [Facebook Developer Community](https://www.facebook.com/groups/fbdevelopers/) group in which you can ask questions and gather feedback. This group is monitored by Facebook staff, and while I didn't get an answer to every question I asked there, one of Facebook's staff was able to help me past one very confusing roadblock that might have had me stumped for days otherwise. If you get stuck, consider asking a question in that group.

## Double Check Your Business Use Setting

According to a Facebook staff member I spoke with in the group above, if you have your app configured for a business-to-business use case, then Business verification will be required for _any_ permissions you request - even those permissions which would not normally require Business Verification.

![Image may contain: text](https://scontent-dfw5-2.xx.fbcdn.net/v/t1.0-9/51807934_10218121295533315_1616040689898881024_n.jpg?_nc_cat=100&_nc_ht=scontent-dfw5-2.xx&oh=a1b0a0311d107851e6ca62189b76573d&oe=5CE6CDAF)

This one caught me off guard since it wasn't clear based on the Business Use options that individual developers not representing any business are meant to select "Support my own business" here. Selecting "Provide services to other businesses" indicates to Facebook that your target use-case is business-to-business which requires Business Verification.

## Know About Test Apps

This one is crucial - the first time I applied for the user\_link permission, I simply described how the permission would be used. There was no way for my app to request the permission, even from my [Test Users](https://developers.facebook.com/docs/apps/test-users), so I was surprised to have my application rejected saying that I must show a live demo of the feature - at first I really wasn't sure how to even go about fulfilling this request.

It took me quite some time to find, and Facebook's documentation doesn't really point you toward it, but [Test Apps](https://developers.facebook.com/docs/apps/test-apps/) are the solution to this issue. You can create a Test App associated with your app account. Test Apps can never be set to Live mode - meaning that real Facebook users will never be able to actually use them. But they can be used by your test users, and have access to every permission which allows you to use the App ID and Secret for your Test App to create a live demo of any permission you wish to request, and allow Facebook to test it in a live environment during app review.

## Don't Ask the Reviewer to Post Data to Your Website

Despite clear instructions to do so, I had my app rejected 4 times without much explanation when I asked the instructors to create a new post on my website using a test user which would have included the test user's name and a link to their profile. You get very little feedback when your app is rejected - usually just "we couldn't see how the permission is being used" with no further explanation.

![](images/unknown.png)

Sometimes you'll be lucky and they will include a screenshot. I've concluded that the reviewers are not allowed to submit data to the websites they are reviewing - which were key steps in my instructions to them. It seems that once they got to steps they weren't allowed to do, they simply ignored my instructions and clicked around the site a bit, hoping to find the permission in use, and then gave me a cookie-cutter rejection notice, occasionally with a screenshot of the wrong page or logged in as the wrong user.

During the final review, I simply created an event on the website myself and shared a link to it, demonstrating that my user's name linked to their Facebook profile, and my application was approved upon verifying that the link worked.

## Be Explicit About Which Test App/User the Reviewer Should Use in Your Instructions

In one of my rejections, I was given a screenshot of the error page that a user sees when attempting to follow a profile link issued to a Test App when logged in as a real Facebook user. This indicates that the reviewer was testing with a real Facebook account, and that they had ignored the selection in the App Verification pane where you can provide a Test App name.

![](images/unknown.png)

This may be in part because the UI of that page is broken - the Test User field autocompletes with test user names, but only from your main app, and not the selected Test App. Since Test Users of your live app can't use your Test App, I'm not sure exactly how this was meant to be used. But in my application which was accepted, I simply indicated which Test App and Test User should be used in the step-by-step instructions I provided, and that seems to have done the trick.

![](images/unknown.png)

## Conclusion

I hope that these tips help ease the experience of anyone else attempting to get a Facebook App Reviewed for a new permission. Ultimately the experience was extremely frustrating for me and ended up spanning more than two weeks from when I first applied to when my app was approved. But hopefully by following these tips and reading the linked documentation, things will go smoother for you!
