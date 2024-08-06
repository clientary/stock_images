# stock_images

Stock images (currently only used for contract/proposal cover page)

## Licenses

https://www.pexels.com/license/

* All photos and videos on Pexels are free to use.
* Attribution is not required. Giving credit to the photographer or Pexels is not necessary but always appreciated.
* You can modify the photos and videos from Pexels. Be creative and edit them as you like.

https://unsplash.com/license

* All images can be downloaded and used for free
* Commercial and non-commercial purposes
* No permission needed (though attribution is appreciated!)

https://pixabay.com/service/license-summary/

*	Use Content for free
*	Use Content without having to attribute the author (although giving credit is always appreciated by our community!)
*	Modify or adapt Content into new works

## How to add more

1. download the highest quality image from pexels/unsplash/pixabay
2. update this README
   - put the url of the source image at the appropriate category at the bottom of this README file
3. generate the "hero" image
   1. use Photoshop to crop image to 1502x939 and export as 100% quality JPG
   2. use any online image optimizer to reduce the file size (I use https://tinyjpg.com/ )
4. generate the "sprite" image
   1. resize the 1502x939 image to 120x75 and export it
5. generate the sprite CSS and sprite PNG
   1. use https://instantsprite.com/
      - this is the fastest site, since it does everything client-side (so no need to upload files to a server)
      - it also generates CSS that you can copypaste with minimal modification
   2. use https://tinypng.com/ to reduce the sprite PNG file size (I went from 1.5 MB to 354 KB)
   3. copypasta the sprite CSS to `StockImagePicker.jsx`
6. update our redirect
   1. upload the "hero" image, the "sprite" image, and the sprite PNG to this repo
   2. go to `https://github.com/clientary/stock_images/tree/[commit hash]/cover_pages`
   3. find the newly uploaded "hero" image, right click, and copy the url
      - the url should look like `https://github.com/clientary/stock_images/blob/[commit hash]/cover_pages/[filename].jpg`
   4. go to https://statically.io/convert/ and paste the url to generate the CDN url
   5. copypasta the CDN url into `app_controller.rb`

Aside: why do we use 1502x939?
- 16:10 is a good ratio
- vertical images don't look so good on Spartan cover page design
- although 4:3 ratio might be better for Impact and Circular, it is still a bit too vertical for Spartan
- minimum image width should be 1502px since that is double 751px (PDF `<body>` width)
  - XREF: paperize-margin-calc
  - XREF: paperize-sheet-heights

## Technical details

We use https://statically.io/ as the CDN because it is free and has unlimited traffic.

Note I couldn't get their "image" CDN to work (if you dig around enough, you'll see [Statically for Wordpress](https://statically.io/wordpress/) which requires applying for an API key. I have a feeling the "image" CDN has a similar requirement)

Buuuuuuut "staticzap" can CDN-ize files on Github .... so we host the stock images on Github

## Account service categories (cover page)

### actual design/engineering/science
'design-eng-science'

Architecture and Design
Interior Design
Industrial Design
Product Design

https://www.pexels.com/photo/silver-imac-on-top-of-brown-wooden-table-326502/
https://www.pexels.com/photo/notebook-beside-the-iphone-on-table-196644/
https://www.pexels.com/photo/person-sitting-facing-laptop-computer-with-sketch-pad-57690/
https://www.pexels.com/photo/white-printer-paper-196645/
https://www.pexels.com/photo/person-holding-apple-magic-mouse-392018/
https://www.pexels.com/photo/man-sitting-in-front-of-computer-380769/
https://www.pexels.com/photo/blue-pen-beside-black-smartphone-on-white-paper-196646/
https://www.pexels.com/photo/turned-on-screen-silver-macbook-air-on-wooden-desk-56759/
https://www.pexels.com/photo/house-floor-plan-271667/
https://www.pexels.com/photo/turned-on-gray-laptop-computer-on-table-699459/
https://www.pexels.com/photo/turned-on-gray-laptop-computer-on-table-699459/
https://unsplash.com/photos/person-writing-on-white-paper-gcsNOsPEXfs
https://unsplash.com/photos/silver-macbook-air-on-table-near-imac-jJT2r2n7lYA
https://unsplash.com/photos/black-smartphone-near-person-5QgIuuBxKwM
https://unsplash.com/photos/a-macbook-with-lines-of-code-on-its-screen-on-a-busy-desk-m_HRfLhgABo
https://unsplash.com/photos/man-writing-on-paper-in-front-of-dslr-mGH253KbfaY

Engineering
Structural Engineering
Chemical Engineering
Environmental Engineering
Civil Engineering
Mechanical Engineering
Electrical Engineering

https://www.pexels.com/photo/three-yellow-and-red-tower-cranes-under-clear-blue-sky-224924/
https://www.pexels.com/photo/low-angle-photography-of-orange-excavator-under-white-clouds-1078884/

Research and Development
Research and Development Labs
Scientific Research

https://www.pexels.com/photo/close-up-of-microscope-256262/
https://www.pexels.com/photo/clear-water-drops-132477/
https://www.pexels.com/photo/person-holding-laboratory-flask-2280571/
https://unsplash.com/photos/five-green-plants-UmncJq4KPcA
https://unsplash.com/photos/purple-and-pink-plasma-ball-OgvqXGL7XO4
https://unsplash.com/photos/white-microscope-on-top-of-black-table-gKUC4TMhOiY


### tech
'tech'

Web Development
Software Development
App Development
Software Testing and QA
Mobile App Development
E-commerce Solutions
SEO Services
Blockchain Consulting
IT Services
IT Consulting

https://unsplash.com/photos/laptop-computer-on-glass-top-table-hpjSkU2UYSU
https://unsplash.com/photos/people-sitting-down-near-table-with-assorted-laptop-computers-SYTO3xs06fU
https://unsplash.com/photos/macro-photography-of-black-circuit-board-FO7JIlwjOtU
https://unsplash.com/photos/monitor-showing-java-programming-OqtafYT5kTw


### health
'health'

Healthcare Consulting
Nursing Services
Pharmacy Services
Physical Therapy
Healthcare and Medical Services
Medical and Dental Practices
Pharmaceutical Services
Fitness and Wellness Services

https://www.pexels.com/photo/low-angle-view-of-woman-relaxing-on-beach-against-blue-sky-317157/
https://www.pexels.com/photo/three-women-s-doing-exercises-863977/
https://www.pexels.com/photo/green-blue-and-pink-kettle-bells-on-blue-surface-221247/
https://www.pexels.com/photo/black-dumbbell-lot-260352/
https://unsplash.com/photos/person-wearing-orange-and-gray-nike-shoes-walking-on-gray-concrete-stairs-PHIgYUGQPvU
https://unsplash.com/photos/woman-doing-exercise-routine-Tq9Ln3gpiG4


### money
'financial'

Accounting
Financial Services
Financial Analysis
Investment Management
Insurance Services
Financial Planning
Investment Banking
Tax Services
Public Accounting
Insurance Brokers
Actuarial Services
Real Estate Services

https://www.pexels.com/photo/rolled-20-u-s-dollar-bill-164527/
https://www.pexels.com/photo/bitcoins-and-u-s-dollar-bills-730547/
https://www.pexels.com/photo/coins-on-brown-wood-210600/
https://www.pexels.com/photo/person-putting-coin-in-a-piggy-bank-3943723/
https://www.pexels.com/photo/black-calculator-near-ballpoint-pen-on-white-printed-paper-53621/
https://unsplash.com/photos/fan-of-100-us-dollar-banknotes-lCPhGxs7pww
https://unsplash.com/photos/selective-focus-photography-of-graph-ZzOa5G8hSPI
https://unsplash.com/photos/green-plant-on-brown-round-coins-lZ_4nPFKcV8


### advertising/media/marketing/content
'advert-media-marketing-content'

Marketing and Advertising
Digital Marketing
Advertising Agencies
Digital Advertising
Social Media Marketing
Brand Strategy
Social Media Influencer Marketing
Media and Entertainment Services
Media Production
Copy Editing and Proofreading
Video Editing
Broadcasting and Media Services
Content Writing and Copywriting
Photography and Videography
Social Media Management
Graphic Design

https://www.pexels.com/photo/two-white-printer-papers-near-macbook-on-brown-surface-590016/
https://www.pexels.com/photo/people-having-a-handshake-7710082/
https://unsplash.com/photos/person-writing-on-white-paper-U33fHryBYBU
https://unsplash.com/photos/white-printing-paper-with-marketing-strategy-text-yktK2qaiVHI
https://unsplash.com/photos/assorted-color-abstract-painting-tZc3vjPCk-Q
https://unsplash.com/photos/three-men-sitting-on-chair-beside-tables-mpN7xjKQ_Ns
https://unsplash.com/photos/three-men-sitting-while-using-laptops-and-watching-man-beside-whiteboard-wD1LRb9OeEo
https://unsplash.com/photos/a-close-up-of-a-computer-screen-with-a-blurry-background-oMe_FjZnHGU
https://unsplash.com/photos/a-computer-screen-with-a-bunch-of-data-on-it-bf9sZBcGQl4


### law/hr
'law-hr'

Legal Services
Legal Consultancy
Corporate Law
Intellectual Property Law
Employment Law
Contract Law
Risk Management

Human Resources and Recruitment
HR Consulting


### business/catch all
'business-etc'

Consulting
Management Consulting
Public Policy Consulting
Supply Chain and Logistics Services
Logistics and Freight Services
Transportation and Logistics Consulting
Translation and Localization Services
Data Analysis and Analytics
Data Science and Analytics
Education and Training
Public Speaking and Training
Public Relations
Business Coaching
Market Research
Market Analysis

Life Coaching
Marketplace Development
Event Planning
Event Promotion
Event Management
Environmental Services
Environmental Consulting
Public Affairs
Social Services
Urban Planning

https://unsplash.com/photos/person-writing-on-white-paper-GJao3ZTX9gU
https://unsplash.com/photos/black-and-silver-fountain-pen-hjwKMkehBco
https://unsplash.com/photos/assorted-title-of-books-piled-in-the-shelves-NIJuEQw0RKg
https://unsplash.com/photos/books-in-glass-bookcase-jKU2NneZAbI
https://unsplash.com/photos/low-angle-photography-of-beige-building-bAQH53VquTc
https://unsplash.com/photos/gray-pillars-Vq__yk6faOI
https://unsplash.com/photos/book-lot-on-black-wooden-shelf-zeH-ljawHtg
https://unsplash.com/photos/woman-holding-sword-statue-during-daytime-DZpc4UY8ZtY
https://www.pexels.com/photo/wooden-gavel-on-wooden-surface-5668802/
https://www.pexels.com/photo/close-up-photo-of-wooden-gavel-5668473/
https://www.pexels.com/photo/judges-desk-with-gavel-and-scales-5669619/
https://www.pexels.com/photo/crop-businessman-giving-contract-to-woman-to-sign-3760067/
https://www.pexels.com/photo/white-printer-paper-48195/

https://www.pexels.com/photo/white-rolling-armchair-beside-table-1957478/
https://www.pexels.com/photo/person-sitting-facing-laptop-computer-with-sketch-pad-57690/
https://www.pexels.com/photo/group-of-friends-hanging-out-933964/
https://www.pexels.com/photo/woman-wearing-gray-blazer-writing-on-dry-erase-board-1181534/
https://www.pexels.com/photo/three-woman-sitting-on-white-chair-in-front-of-table-2041627/
https://www.pexels.com/photo/person-holding-document-papers-259006/
https://www.pexels.com/photo/man-and-woman-holding-each-other-s-hands-as-a-team-5256816/
https://unsplash.com/photos/a-person-sitting-at-a-table-with-a-laptop-oUbzU87d1Gc
https://unsplash.com/photos/man-standing-in-front-of-group-of-men-rxpThOwuVgE
https://unsplash.com/photos/group-of-people-using-laptop-computer-QckxruozjRg
https://unsplash.com/photos/person-writing-on-brown-wooden-table-near-white-ceramic-mug-s9CC2SKySJM
https://unsplash.com/photos/oval-brown-wooden-conference-table-and-chairs-inside-conference-room-GWe0dlVD9e0
https://unsplash.com/photos/people-sitting-down-near-table-with-assorted-laptop-computers-SYTO3xs06fU
https://unsplash.com/photos/depth-of-field-photography-of-man-playing-chess-fzOITuS1DIQ
https://unsplash.com/photos/person-reading-book-RX_0vwSPiWs
https://unsplash.com/photos/a-group-of-people-putting-their-hands-together-YjWzTTrnwQw
