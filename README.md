# include-workflow

This is an action that allows you to abuse [Composite Actions](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action) to include workflows steps 

1. Add shared workflow steps, for example in your repository:
   `.github/workflows/shared/snippet.yml`
   ```yaml
       - run: echo "This step is shared!"
         shell: bash
       - uses: vincetse/fortune-cookie-action@v3
   ```
   
2. In the workflow where you want to include the steps, add a step:
   ```yaml
    - uses: cschleiden/include-workflow@main
      with:
        workflow-steps: ${{ github.workspace }}/.github/workflows/shared/snippet.yml
   ```
3. Run your workflow!

4. Bonus: add 
   ```yaml
    - uses: cschleiden/include-workflow@main
      with:
        workflow-steps: ${{ github.workspace }}/.github/workflows/shared/snippet.yml
   ```
   to **another** workflow.

5. Update `.github/workflows/shared/snippet.yml` and re-run the workflows including it, they'll now run the updated steps from the shared snippe! 🎉🥳

Example: https://github.com/cschleiden/include-workflow-test/actions/runs/1167755605 
