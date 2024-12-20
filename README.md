# GITHUB ACTIONS

This has been edited on behalf of 05-1 action.

### Context

- Access information about runs, variables, jobs and much more → sources of data

- We can provide all the necessary information to our workloads
  Not every context is available at every step of the job

- There are many contexts like github, env, inputs, vars, secrets, matrix etc. Fortunately, with the help of VScode Github action extension, it tells us which ones we could use.

### Variable

- Single workflow variable

  - workflow, job and step level

    ```bash
    echo "Hello $NAME!"
    ```

- Multiple workflows variable

  - organization, repository and enviornment level

    ```bash
    echo "Hello ${{vars.NAME}}!"
    # vars context으로 접근해야 한다.
    ```

    ![Environment, Repository and Organization variables](https://github.com/user-attachments/assets/22633e94-5416-4ff5-8693-d07827885df5)

    - Organization 만들고, organization value를 만들기 위해 리포지토리를 organization으로 옮김
    - Repository variables은 Repo에서 설정가능
    - Enviornment variables은 dev, prod, staging같은 각각의 환경에서 쓰이는 변수

### Function

- General purpose functions(methods)

  - utility functions to interact with data from contexts, and model more complex behavior like more advanced control workflow and job execution
    ```
    contains()
    startsWith()
    endsWith()
    fromJSON() → Deserialize, env변수를 가져올때도 사용한다
    toJSON() → Serialize
    hashFiles()
    ...
    ```

- Status check functions
  - Functions that can use the status of the workflow, previous jobs or steps to define whether a certain job or step should be executed
    ```
    success() → previous jobs or steps all succeeded?
    failure() → any of them failed?
    cancelled() →
    always()
    ```

PR trigger해서 github.context.event.pull_request invoke하기

### Artifacts

- Stored for up to 90 days
- Managed via 2 actions
  - upload-artifact
  - download-artifact
    - 같은 workflow에서 업로드된 artifact만 다운로드 가능하다다
- Recommended when the stored files are likely to be accessed outside the workflow, for example
  - Build outupus
  - Test results
  - Logs
  - Uploading and downloading the build outputs for deployments

### Caching

- Stored for up to 7 days
- Managed via a single action
  - cache
- Recommended when the stored files are likely to be accessed only within the workflow, for example
  - Build dependencies
