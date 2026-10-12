# stock_images

Stock photos for contract and proposal cover pages in Clientary: the gallery in the cover page builder, and the covers of the template directory's templates.

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

## What's here

- `cover_pages/`: each photo as a cover, 1502x939, a progressive JPEG at quality 76.
- `cover_pages_thumbnail/`: each photo at 120x75, for the gallery.
- `cover_page_sprite.png`: the thumbnails in one image for the gallery, stacked top to bottom with a 1px transparent gap, so the tile at position n (from 0) starts n x 76px down. Its order is the order of the sprite CSS in `StockImagePicker.js.jsx`, and a new photo goes at the end.

In the app (ronin):

- `AppController::STOCK_IMAGE_URLS` (`app_controller.rb`) maps each photo's name to its CDN URL, `https://cdn.statically.io/gh/clientary/stock_images/[commit hash]/cover_pages/[name].jpg`, pinned to the commit that added it.
- `StockImagePicker.js.jsx` lists each photo with its tags, and holds the sprite CSS. A photo's tags are business types and categories from `RoninConstants.DEFAULT_SERVICE_TYPES`, and the gallery recommends photos tagged with an account's business type or its category first.

## How to add more

1. Download the highest quality original from Pexels, Unsplash, or Pixabay, and name it as the others are: `pexels-[photographer]-[id].jpg`, or `[photographer]-[id]-unsplash.jpg`.
2. Make the cover, cropped from the center (check the subject stays in frame, and crop by hand if it doesn't):
   ```
   convert original.jpg -auto-orient -resize "1502x939^" -gravity center -extent 1502x939 -strip -quality 76 -interlace JPEG cover_pages/[name].jpg
   ```
3. Make the thumbnail:
   ```
   convert cover_pages/[name].jpg -resize "120x75!" -quality 92 cover_pages_thumbnail/[name].jpg
   ```
4. Add the thumbnail to the end of the sprite, then bring it back to 256 colors. Leave dithering off: with one palette shared by every photo, dithering speckles the new ones.
   ```
   convert cover_page_sprite.png "(" -size 120x1 xc:none ")" cover_pages_thumbnail/[name].jpg -background none -append PNG32:sprite_full.png
   convert sprite_full.png +dither -colors 256 PNG8:cover_page_sprite.png
   ```
5. List the photo below, under the first category in its tags, with its source URL.
6. Commit and push here, then in ronin:
   - add the photo's CDN URL, at the new commit, to `STOCK_IMAGE_URLS`, and point `stock-sprite` at the new commit
   - add the photo to `StockImagePicker.js.jsx`: its path and tags in the list, and its sprite CSS line, `background-position: 0 -[n x 76]px`
7. Prime the CDN's cache: open the new cover's URL and the sprite's URL once, and check each loads.

ImageMagick's `convert` is in the ronin Vagrant VM. Photoshop, https://tinyjpg.com/, and https://instantsprite.com/ do the same job by hand.

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

## Photos by category

Each photo is listed once, under the first category in its tags, with the other categories it's tagged with. The business types are each category's in `RoninConstants.DEFAULT_SERVICE_TYPES`.

### Design, engineering, and science
`'design-eng-science'`

Business types: Architecture and Design, Interior Design, Industrial Design, Product Design, Engineering, Structural Engineering, Chemical Engineering, Environmental Engineering, Civil Engineering, Mechanical Engineering, Electrical Engineering, Research and Development, Research and Development Labs, Scientific Research

- `alexandre-debieve-FO7JIlwjOtU-unsplash.jpg`: https://unsplash.com/photos/macro-photography-of-black-circuit-board-FO7JIlwjOtU (also tech)
- `chuttersnap-UmncJq4KPcA-unsplash.jpg`: https://unsplash.com/photos/five-green-plants-UmncJq4KPcA
- `hal-gatewood-OgvqXGL7XO4-unsplash.jpg`: https://unsplash.com/photos/purple-and-pink-plasma-ball-OgvqXGL7XO4
- `ousa-chea-gKUC4TMhOiY-unsplash.jpg`: https://unsplash.com/photos/white-microscope-on-top-of-black-table-gKUC4TMhOiY
- `pexels-chokniti-khongchum-1197604-2280571.jpg`: https://www.pexels.com/photo/person-holding-laboratory-flask-2280571/
- `pexels-d-goug-211350543-27938317.jpg`: https://www.pexels.com/photo/new-home-constructions-27938317/
- `pexels-falling4utah-2724748.jpg`: https://www.pexels.com/photo/kitchen-with-furniture-and-appliances-2724748/
- `pexels-inspiredimages-132477.jpg`: https://www.pexels.com/photo/clear-water-drops-132477/
- `pexels-pixabay-256262.jpg`: https://www.pexels.com/photo/close-up-of-microscope-256262/
- `pexels-pixabay-271667.jpg`: https://www.pexels.com/photo/house-floor-plan-271667/
- `pexels-rezwan-1078884.jpg`: https://www.pexels.com/photo/low-angle-photography-of-orange-excavator-under-white-clouds-1078884/
- `pexels-valentin-ivantsov-2154772556-36035073.jpg`: https://www.pexels.com/photo/modern-interior-kitchen-under-renovation-36035073/
- `pexels-wdnet-224924.jpg`: https://www.pexels.com/photo/three-yellow-and-red-tower-cranes-under-clear-blue-sky-224924/

### Tech
`'tech'`

Business types: Web Development, Software Development, App Development, Software Testing and QA, Mobile App Development, E-commerce Solutions, SEO Services, Blockchain Consulting, IT Services, IT Consulting

- `austin-distel-RX_0vwSPiWs-unsplash.jpg`: https://unsplash.com/photos/person-reading-book-RX_0vwSPiWs (also advert-media-marketing-content)
- `christopher-gower-m_HRfLhgABo-unsplash.jpg`: https://unsplash.com/photos/a-macbook-with-lines-of-code-on-its-screen-on-a-busy-desk-m_HRfLhgABo
- `firmbee-com-gcsNOsPEXfs-unsplash.jpg`: https://unsplash.com/photos/person-writing-on-white-paper-gcsNOsPEXfs (also financial, advert-media-marketing-content)
- `ilya-pavlov-OqtafYT5kTw-unsplash.jpg`: https://unsplash.com/photos/monitor-showing-java-programming-OqtafYT5kTw

### Health
`'health'`

Business types: Healthcare Consulting, Nursing Services, Pharmacy Services, Physical Therapy, Healthcare and Medical Services, Medical and Dental Practices, Pharmaceutical Services, Fitness and Wellness Services

- `bruno-nascimento-PHIgYUGQPvU-unsplash.jpg`: https://unsplash.com/photos/person-wearing-orange-and-gray-nike-shoes-walking-on-gray-concrete-stairs-PHIgYUGQPvU
- `pexels-chevanon-317157.jpg`: https://www.pexels.com/photo/low-angle-view-of-woman-relaxing-on-beach-against-blue-sky-317157/
- `pexels-olly-863977.jpg`: https://www.pexels.com/photo/three-women-s-doing-exercises-863977/
- `pexels-pixabay-221247.jpg`: https://www.pexels.com/photo/green-blue-and-pink-kettle-bells-on-blue-surface-221247/
- `pexels-pixabay-260352.jpg`: https://www.pexels.com/photo/black-dumbbell-lot-260352/
- `rima-kruciene-Tq9Ln3gpiG4-unsplash.jpg`: https://unsplash.com/photos/woman-doing-exercise-routine-Tq9Ln3gpiG4

### Money
`'financial'`

Business types: Accounting, Financial Services, Financial Analysis, Investment Management, Insurance Services, Financial Planning, Investment Banking, Tax Services, Public Accounting, Insurance Brokers, Actuarial Services, Real Estate Services

- `alexander-mils-lCPhGxs7pww-unsplash.jpg`: https://unsplash.com/photos/fan-of-100-us-dollar-banknotes-lCPhGxs7pww
- `m-ZzOa5G8hSPI-unsplash.jpg`: https://unsplash.com/photos/selective-focus-photography-of-graph-ZzOa5G8hSPI
- `micheile-henderson-lZ_4nPFKcV8-unsplash.jpg`: https://unsplash.com/photos/green-plant-on-brown-round-coins-lZ_4nPFKcV8
- `microsoft-365-oUbzU87d1Gc-unsplash.jpg`: https://unsplash.com/photos/a-person-sitting-at-a-table-with-a-laptop-oUbzU87d1Gc (also business-etc)
- `pexels-cottonbro-3943723.jpg`: https://www.pexels.com/photo/person-putting-coin-in-a-piggy-bank-3943723/
- `pexels-davidmcbee-730547.jpg`: https://www.pexels.com/photo/bitcoins-and-u-s-dollar-bills-730547/
- `pexels-n-voitkevich-6863330.jpg`: https://www.pexels.com/photo/person-filing-tax-documents-6863330/
- `pexels-pixabay-164527.jpg`: https://www.pexels.com/photo/rolled-20-u-s-dollar-bill-164527/
- `pexels-pixabay-210600.jpg`: https://www.pexels.com/photo/coins-on-brown-wood-210600/
- `pexels-pixabay-259006.jpg`: https://www.pexels.com/photo/person-holding-document-papers-259006/ (also business-etc)
- `pexels-pixabay-53621.jpg`: https://www.pexels.com/photo/black-calculator-near-ballpoint-pen-on-white-printed-paper-53621/

### Advertising, media, marketing, and content
`'advert-media-marketing-content'`

Business types: Marketing and Advertising, Market Research, Market Analysis, Digital Marketing, Advertising Agencies, Digital Advertising, Social Media Marketing, Brand Strategy, Social Media Influencer Marketing, Media and Entertainment Services, Media Production, Copy Editing and Proofreading, Video Editing, Broadcasting and Media Services, Content Writing and Copywriting, Photography and Videography, Social Media Management, Graphic Design

- `1981-digital-bf9sZBcGQl4-unsplash.jpg`: https://unsplash.com/photos/a-computer-screen-with-a-bunch-of-data-on-it-bf9sZBcGQl4 (also tech, business-etc, design-eng-science)
- `1981-digital-oMe_FjZnHGU-unsplash.jpg`: https://unsplash.com/photos/a-close-up-of-a-computer-screen-with-a-blurry-background-oMe_FjZnHGU (also tech, business-etc, design-eng-science)
- `annie-spratt-QckxruozjRg-unsplash.jpg`: https://unsplash.com/photos/group-of-people-using-laptop-computer-QckxruozjRg (also business-etc, tech)
- `austin-distel-mpN7xjKQ_Ns-unsplash.jpg`: https://unsplash.com/photos/three-men-sitting-on-chair-beside-tables-mpN7xjKQ_Ns (also business-etc, tech)
- `austin-distel-rxpThOwuVgE-unsplash.jpg`: https://unsplash.com/photos/man-standing-in-front-of-group-of-men-rxpThOwuVgE (also business-etc, tech)
- `austin-distel-wD1LRb9OeEo-unsplash.jpg`: https://unsplash.com/photos/three-men-sitting-while-using-laptops-and-watching-man-beside-whiteboard-wD1LRb9OeEo (also business-etc, tech)
- `brad-neathery-mGH253KbfaY-unsplash.jpg`: https://unsplash.com/photos/man-writing-on-paper-in-front-of-dslr-mGH253KbfaY
- `campaign-creators-yktK2qaiVHI-unsplash.jpg`: https://unsplash.com/photos/white-printing-paper-with-marketing-strategy-text-yktK2qaiVHI
- `carlos-muza-hpjSkU2UYSU-unsplash.jpg`: https://unsplash.com/photos/laptop-computer-on-glass-top-table-hpjSkU2UYSU (also financial, tech, business-etc)
- `hal-gatewood-tZc3vjPCk-Q-unsplash.jpg`: https://unsplash.com/photos/assorted-color-abstract-painting-tZc3vjPCk-Q (also tech)
- `headway-5QgIuuBxKwM-unsplash.jpg`: https://unsplash.com/photos/black-smartphone-near-person-5QgIuuBxKwM (also business-etc)
- `melanie-deziel-U33fHryBYBU-unsplash.jpg`: https://unsplash.com/photos/person-writing-on-white-paper-U33fHryBYBU (also business-etc)
- `pexels-a-darmel-7710082.jpg`: https://www.pexels.com/photo/people-having-a-handshake-7710082/ (also business-etc)
- `pexels-caio-56759.jpg`: https://www.pexels.com/photo/turned-on-screen-silver-macbook-air-on-wooden-desk-56759/
- `pexels-flodahm-699459.jpg`: https://www.pexels.com/photo/turned-on-gray-laptop-computer-on-table-699459/
- `pexels-fotios-photos-1957478.jpg`: https://www.pexels.com/photo/white-rolling-armchair-beside-table-1957478/ (also business-etc)
- `pexels-knownasovan-57690.jpg`: https://www.pexels.com/photo/person-sitting-facing-laptop-computer-with-sketch-pad-57690/
- `pexels-picjumbo-com-55570-196644.jpg`: https://www.pexels.com/photo/notebook-beside-the-iphone-on-table-196644/ (also tech)
- `pexels-picjumbo-com-55570-196645.jpg`: https://www.pexels.com/photo/white-printer-paper-196645/ (also tech)
- `pexels-picjumbo-com-55570-196646.jpg`: https://www.pexels.com/photo/blue-pen-beside-black-smartphone-on-white-paper-196646/ (also tech)
- `pexels-tranmautritam-326502.jpg`: https://www.pexels.com/photo/silver-imac-on-top-of-brown-wooden-table-326502/ (also business-etc)
- `pexels-vojtech-okenka-127162-392018.jpg`: https://www.pexels.com/photo/person-holding-apple-magic-mouse-392018/ (also business-etc, tech, design-eng-science)
- `unseen-studio-s9CC2SKySJM-unsplash.jpg`: https://unsplash.com/photos/person-writing-on-brown-wooden-table-near-white-ceramic-mug-s9CC2SKySJM (also business-etc)
- `ux-store-jJT2r2n7lYA-unsplash.jpg`: https://unsplash.com/photos/silver-macbook-air-on-table-near-imac-jJT2r2n7lYA (also tech, design-eng-science)

### Law and HR
`'law-hr'`

Business types: Legal Services, Legal Consultancy, Corporate Law, Intellectual Property Law, Employment Law, Contract Law, Risk Management, Human Resources and Recruitment, HR Consulting

- `alvaro-serrano-hjwKMkehBco-unsplash.jpg`: https://unsplash.com/photos/black-and-silver-fountain-pen-hjwKMkehBco
- `claire-anderson-Vq__yk6faOI-unsplash.jpg`: https://unsplash.com/photos/gray-pillars-Vq__yk6faOI
- `clarisse-meyer-jKU2NneZAbI-unsplash.jpg`: https://unsplash.com/photos/books-in-glass-bookcase-jKU2NneZAbI (also business-etc)
- `cytonn-photography-GJao3ZTX9gU-unsplash.jpg`: https://unsplash.com/photos/person-writing-on-white-paper-GJao3ZTX9gU (also business-etc)
- `giammarco-boscaro-zeH-ljawHtg-unsplash.jpg`: https://unsplash.com/photos/book-lot-on-black-wooden-shelf-zeH-ljawHtg
- `pexels-pixabay-48195.jpg`: https://www.pexels.com/photo/white-printer-paper-48195/
- `pexels-sora-shimazaki-5668473.jpg`: https://www.pexels.com/photo/close-up-photo-of-wooden-gavel-5668473/
- `pexels-sora-shimazaki-5669619.jpg`: https://www.pexels.com/photo/judges-desk-with-gavel-and-scales-5669619/
- `sebastian-pichler-bAQH53VquTc-unsplash.jpg`: https://unsplash.com/photos/low-angle-photography-of-beige-building-bAQH53VquTc
- `tingey-injury-law-firm-DZpc4UY8ZtY-unsplash.jpg`: https://unsplash.com/photos/woman-holding-sword-statue-during-daytime-DZpc4UY8ZtY

### Business and everything else
`'business-etc'`

Business types: Consulting, Management Consulting, Public Policy Consulting, Supply Chain and Logistics Services, Logistics and Freight Services, Transportation and Logistics Consulting, Translation and Localization Services, Data Analysis and Analytics, Data Science and Analytics, Education and Training, Public Speaking and Training, Public Relations, Business Coaching, Life Coaching, Marketplace Development, Event Planning, Event Promotion, Event Management, Environmental Services, Environmental Consulting, Public Affairs, Social Services, Urban Planning

- `benjamin-child-GWe0dlVD9e0-unsplash.jpg`: https://unsplash.com/photos/oval-brown-wooden-conference-table-and-chairs-inside-conference-room-GWe0dlVD9e0 (also advert-media-marketing-content, design-eng-science, tech)
- `jeshoots-com-fzOITuS1DIQ-unsplash.jpg`: https://unsplash.com/photos/depth-of-field-photography-of-man-playing-chess-fzOITuS1DIQ
- `marvin-meyer-SYTO3xs06fU-unsplash.jpg`: https://unsplash.com/photos/people-sitting-down-near-table-with-assorted-laptop-computers-SYTO3xs06fU (also advert-media-marketing-content)
- `meghan-lamle-YjWzTTrnwQw-unsplash.jpg`: https://unsplash.com/photos/a-group-of-people-putting-their-hands-together-YjWzTTrnwQw (also advert-media-marketing-content)
- `pexels-cowomen-1058097-2041627.jpg`: https://www.pexels.com/photo/three-woman-sitting-on-white-chair-in-front-of-table-2041627/ (also advert-media-marketing-content)
- `pexels-divinetechygirl-1181534.jpg`: https://www.pexels.com/photo/woman-wearing-gray-blazer-writing-on-dry-erase-board-1181534/ (also advert-media-marketing-content)
- `pexels-olly-3760067.jpg`: https://www.pexels.com/photo/crop-businessman-giving-contract-to-woman-to-sign-3760067/
- `pexels-seven11nash-380769.jpg`: https://www.pexels.com/photo/man-sitting-in-front-of-computer-380769/ (also advert-media-marketing-content, tech)
- `pexels-sora-shimazaki-5668802.jpg`: https://www.pexels.com/photo/wooden-gavel-on-wooden-surface-5668802/ (also advert-media-marketing-content)
- `pexels-thatguycraig000-2306281.jpg`: https://www.pexels.com/photo/tables-with-flower-decors-2306281/
- `pexels-thirdman-5256816.jpg`: https://www.pexels.com/photo/man-and-woman-holding-each-other-s-hands-as-a-team-5256816/ (also advert-media-marketing-content)
- `pexels-wildlittlethingsphoto-933964.jpg`: https://www.pexels.com/photo/group-of-friends-hanging-out-933964/ (also advert-media-marketing-content)
