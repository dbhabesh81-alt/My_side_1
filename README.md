# Portfolio website (3D glass cube hero + admin panel)

Files: `index.html` (website), `admin.html` (admin panel), `data.json` (all editable content), `images/` (uploaded photos).

## Deploy on GitHub Pages
1. Create a new GitHub repository and upload all files (keep the `images` folder).
2. Repo Settings > Pages > Source: "Deploy from a branch" > Branch: `main`, folder `/ (root)` > Save.
3. Site: `https://USERNAME.github.io/REPO/`  Admin: `.../admin.html`

## Admin panel setup
1. GitHub > Settings > Developer settings > Fine-grained tokens > Generate new token.
2. Repository access: only your site repo. Permission: Contents = Read and write.
3. Open `admin.html`, enter username, repo, branch and token, edit, then click "Publish to GitHub".

The 3D cube uses Three.js from a CDN, so visitors need internet access.

## Admin password
Default password: `Pixlo@2026` (change it in the admin panel under 'Admin password', then Publish).
The website itself is open to everyone, no sign-in needed.
Note: the password only locks the admin screen. Real protection for publishing is your GitHub token.

## Chat (optional, admin-only inbox)
Visitors chat from the website; you read and reply only inside admin.html (Chat inbox). It uses a free Firebase Realtime Database:
1. console.firebase.google.com > Add project > Build > Realtime Database > Create database.
2. Rules tab, paste and Publish:
```
{"rules":{"chats":{".read":false,".write":false,"$vid":{".read":true,".write":true,"$mid":{".validate":"newData.hasChildren(['from','text','t']) && newData.child('text').isString() && newData.child('text').val().length < 500"}}}}}
```
3. Copy the database URL (https://...firebaseio.com). In admin.html > Chat: set "Show chat button" to On, paste the URL, then Publish.
4. Project settings > Service accounts > Database secrets: copy the secret and paste it in admin.html > Chat inbox (stays only in your browser).
