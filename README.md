# POC for recreating the expo image problem

What I did is create an apps folder which will contain multiple apps. So the root workspace is `full-poc/` and the workspaces are `apps/*`. Then:
- I cloned the solito with expo router starter template and into `test-app`
- Removed the `.yarn` and `.yarn.lock` files and the `packageManager` key from `test-app/package.json` to use the one of the root workspace (`full-poc/package.json`)
- Updated the workspaceRoot in `metro.config.js` of the expo app to be `path.resolve(projectRoot, '../..')`
- Did `yarn expo install expo-image --yarn` in the `test-app/apps/expo` to download expo-image package and fix the previous error
- Added `.../test-app/packages/app/public/images/test3.jpg` and imported it into `.../test-app/packages/app/features/home/screen.tsx` and used It as a source for the `<SolitoImage />` component
---
On web it is working fine, but by doing `yarn run native` the image doesn't appear

I tried using the `Image` component of expo directly in `.../test-app/apps/expo/app/index.tsx` (and updated the imports) and it is still not showing.
That's why I suspected that It is a bundler problem, maybe not able to bundle the image and ship it to the device. Not sure..
