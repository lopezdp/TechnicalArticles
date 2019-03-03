# ASAPBookings.com UX/UI WebApp Testing & Review

**Reviewer:** David P. Lopez

**Web Application:** https://www.asapbookings.com

**UpWork ContractID:** 21709334

Client need for a QA/QC tester to test a new web application at the website above.

## On Page Load

1. When the page loads for the first time, it loads on the `Register` form, and the title is only underlined as shown in **Image 1** displayed in **Observation 1** below.

2. When the `Register` page is displayed on a mobile device with `screen size < 768px`, the margins can be improved to display a consistent "look and feel" between the header image, the title/tagline text, and the `Register` form itself as discussed in **Observation 2** below.

**Image 1**
![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AsapReviewImg/01.PNG "Image 1")

### Observation 1

When a user clicks on the `Login` tab and reverts back to the `Register` form, the fields are rendered with a light blue background highlight as shown in **Image 2** and **Image 3** below:

**Image 2**

Highlighted `Login` tab:

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AsapReviewImg/02.PNG "Image 2")

**Image 3**

Highlighted `Register` tab:

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AsapReviewImg/03.PNG "Image 3")

### Reviewer Suggestion

Highlight the `Register` tab on the initial page load of the application also to maintain the visual consistency of the different design elements.

### Observation 2

When the `Register` page is displayed on a mobile device, there is an obvious difference in the `margin` settings between the header image, the title/tagline text, and the `Register` form itself.

**Image 4**

Margin differences on `Register` form on a mobile device (iOS):

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AsapReviewImg/04.PNG "Image 4")

### Reviewer Suggestion

Correct `margin` inconsitencies and select a consistent margin setting for each UX element displayed to the device.

## ERROR: Booking Failure

1. When booking an appointment at: `Shareable link www.asapbookings.com/business/lopezdp` I created a booking event for the test profile and the test service and the application returned an **ERROR: Booking Failure** message.

### Observation 1

When a user tries to book an appointment from the `Shareable Link` interface on the web, the user gets a booking error as shown:

**Image 5**

Error message response:

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AsapReviewImg/05.PNG "Image 5")

### Steps to Reproduce

**Image 6**

User enters name:

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AsapReviewImg/06.PNG "Image 6")

**Image 7**

User enters valid phone:

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AsapReviewImg/07.PNG "Image 7")

**Image 8**

User enters valid address:

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AsapReviewImg/08.PNG "Image 8")

### Reviewer Suggestion

Check `backend` logic and debug issue.

## Mobile Responsiveness

1. When the page is viewed on mobile devices iOS, or iPad, the html elements do not properly display the implemented features and elements.

### Observations

**Image 9**

Content is not centered on mobile devices as show:

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AsapReviewImg/09.PNG "Image 9")

**Image 10**

Content is not centered on mobile devices as show (Content as Scrolled down on page):

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AsapReviewImg/10.PNG "Image 10")

**Image 11**

In Landscape, header content and main display content does not share screen appropriately. In landscape design elements for header should change to a smaller height dimension to let main content display more efficiently.

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AsapReviewImg/11.PNG "Image 11")

**Image 12**

On iPad devices in landscape, the design elements in the header do not respect each other and the bug reporting email is hidden from the user behind another element that is layered over the email address.

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AsapReviewImg/12.PNG "Image 12")

### Reviewer Suggestion

For **Image 10** it may be best to separate out the screens to take up one page at a time instead of forcing the user to scroll when on mobile. Separate your booking logic into chunks so that only the pertinent information needed in each step is only shown on the screen without any scrolling. When the user completes the step shown to gather the required info, let the user confirm that they are ready for the information in the next screen, and let the app render a new screen that would avoid the user having to scroll through an infinite form that gives no feedback to the user in regards to their progress when filling out the form.

I would add a progress bar if you change the interface as I have suggested so that the user knows how much is left in the workflow to complete when on mobile.



