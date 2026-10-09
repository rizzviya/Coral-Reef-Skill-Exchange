# My Living Ocean + Skill Challenges

This package contains:

- `my_living_ocean.html` — standalone ocean-builder frontend demo. Open it in a browser to test it.
- `skill_challenges.js` — a reusable JavaScript component for the four reef-coin skill challenges.

## Important integration note

The ocean HTML currently includes a **demo** coin system. The skill-challenge component also supports demo mode. Browser storage and frontend code are not secure enough for real rewards. Before launch, the backend should verify video-call attendance, skill interaction completion, quiz results, and whether hints were used, then update the user's coin balance server-side.

## How to add this to your teammate's GitHub repository

### Option A — easiest: upload files on GitHub website

1. Ask your teammate for the repository link and confirm they are happy for you to contribute. If you do not have write access, use the fork-and-pull-request method below.
2. Download `my_living_ocean.html` and `skill_challenges.js` from this package. Keep `README.md` too if helpful.
3. Open the repository on GitHub and navigate to the folder where your teammate wants the feature. If there is already a frontend folder, use the agreed folder rather than placing files randomly.
4. Click **Add file → Upload files**.
5. Upload `my_living_ocean.html` and `skill_challenges.js` (and optionally this README).
6. In the commit message, enter `Add ocean builder and skill challenge module`.
7. Choose **Create a new branch for this commit and start a pull request** if GitHub offers it. Name the branch `feature/living-ocean`.
8. Click **Propose changes** / **Commit changes**, then create the pull request.
9. Send your teammate the pull-request link. They can review it and click **Merge pull request** when ready.

### Option B — recommended: use Git on your computer

1. Open the repository page on GitHub and click **Fork** if you do not have write access. If you do have write access, ask your teammate whether to create a branch in the original repository.
2. Copy the repository's HTTPS clone URL from **Code**.
3. Open PowerShell in the folder where you keep projects and run:

   ```powershell
   git clone PASTE_REPOSITORY_HTTPS_URL_HERE
   cd REPOSITORY_FOLDER_NAME
   git checkout -b feature/living-ocean
   ```

4. Copy `my_living_ocean.html` and `skill_challenges.js` into the agreed frontend folder in the cloned repository. Do not delete or replace existing project files.
5. Run:

   ```powershell
   git status
   git add path/to/my_living_ocean.html path/to/skill_challenges.js
   git commit -m "Add ocean builder and skill challenge module"
   git push -u origin feature/living-ocean
   ```

   Replace the example paths with the actual paths you used. If Git asks you to sign in, follow GitHub's sign-in flow.
6. Open GitHub. It should offer **Compare & pull request** for your branch. Click it, explain that these are the ocean-builder and skill-challenge frontend files, and create the pull request.
7. Send your teammate the pull-request URL so they can review and merge it.

### If your teammate has not given you repository access

Do not try to push directly to their account. Fork the repository, push your feature branch to your fork, then open a pull request from your fork into your teammate's repository. Your teammate owns the final merge.

## How to use `skill_challenges.js`

Add a container where the challenges should appear and load the script:

```html
<div id="skill-challenges"></div>
<script src="skill_challenges.js"></script>
<script>
  let reefCoins = 120; // Replace with the app's actual wallet state.
  const challengeUI = SkillChallenges.mount({
    container: '#skill-challenges',
    getCoins: () => reefCoins,
    onReward: ({ coins }) => {
      reefCoins += coins;
      // Update the app's wallet display here.
    }
  });
</script>
```

That example uses demo mode. To use real rewards, pass a `verifyChallenge` function that sends the challenge ID to your backend and returns `{ success: true, coinsAwarded: 50 }` only after the backend verifies completion. The backend must enforce one-time claims and calculate/record the real coin reward; do not rely on values sent by the browser.

## Four challenges included

| Challenge | Demo reward |
|---|---:|
| Complete a 1-hour video-call learning session | 50 coins |
| Teach or learn a simple skill in a completed interaction | 20 coins |
| Finish a skill test with every answer correct | 25 coins |
| Finish a skill test without using hints | 15 coins |
