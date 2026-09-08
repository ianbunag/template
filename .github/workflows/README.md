# Workflows

## Sync AGENTS.md to Subscribers

[`sync-agents.yml`](sync-agents.yml) implements a **push-model** synchronization process: whenever `AGENTS.md` is updated on the `main` branch of this template repository, the workflow automatically opens (or updates) a Pull Request in every subscriber repository with the latest version.

### Adding a New Repository

1. Open [`subscribers.txt`](../../subscribers.txt) in the repository root.
2. Add the new repository on its own line in `owner/repo` format:

   ```
   ianbunag/my-new-project
   ```

   Blank lines and lines starting with `#` are ignored.

3. Update the `TARGET_REPO_PAT` token's repository access to include the new repository (see below).
4. Commit and push. The next `AGENTS.md` change will include the new subscriber.

### Managing the `TARGET_REPO_PAT` Secret

The workflow authenticates to subscriber repositories using a **fine-grained Personal Access Token** stored as a repository secret named `TARGET_REPO_PAT`.

#### Creating or Updating the Token

1. Go to **GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens** ([direct link](https://github.com/settings/tokens?type=beta)).
2. Click **Generate new token** (or edit the existing token).
3. Under **Repository access**, select **Only select repositories** and check every repository listed in `subscribers.txt`.
4. Under **Permissions → Repository permissions**, grant:
   - **Contents** — Read and write (to push the sync branch).
   - **Pull requests** — Read and write (to open/list PRs).
   - **Metadata** — Read-only (required by GitHub for all fine-grained tokens).
5. Click **Generate token** and copy the value.
6. Navigate to the template repository's **Settings → Secrets and variables → Actions → Repository secrets**.
7. Create or update the secret named `TARGET_REPO_PAT` with the token value.

#### When You Add a New Subscriber

Every time you add a repository to `subscribers.txt`, you **must** also update the token's selected repository list:

1. Go to **GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens**.
2. Click on the existing token.
3. Under **Repository access**, add the newly subscribed repository.
4. Click **Update token**.

> [!CAUTION]
> **Token Expiration** — GitHub limits fine-grained PATs to a **maximum lifetime of 1 year**. When the token expires, all sync runs will fail silently. Set a calendar reminder to rotate the token before it expires:
>
> 1. Generate a new fine-grained token following the steps above.
> 2. Update the `TARGET_REPO_PAT` secret in the template repository with the new value.
> 3. Revoke the old token.
