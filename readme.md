# Minimal reproduction repo for #10392

Issue: `quarto preview` does not update all pages when project-wide contents change

https://github.com/quarto-dev/quarto-cli/issues/10392

This repo is created by running `quarto create` command > select `book`.

## Prerequisites

1.  Install Quarto.
1.  Clone this repo.

## Steps to reproduce issue

1.  Run `quarto preview`, the preview of the book should display in a browser.
1.  Make edits in `summary.qmd`, save the file.
1.  The following will happen:
    1.  Quarto will attempt to re-render the site.
    1.  The terminal prints the pandoc yaml for the edited file.
    1.  The browser navigates to Summary even though we did not navigate to that page.
1.  The Summary page shown in browser preview is the unedited version.

Attempt to edit `summary.qmd` and save again will repeat the events starting from 3.i.

## Additional information

1.  Setting project > preview > nagivate as `false` does not disable the auto navigate behaviour.

    `_quarto.yml`:
    ```
    project:
        preview:
            navigate: false
    ```

1.
    > ... from #10392
    >
    > ### Actual behavior
    > Changes are effectively made only after stop background job and render the document again.
    >
    > ...

    For my case, without stopping the preview session, saving the `_quarto.yml` file will trigger a refresh that renders the preview correctly again.
