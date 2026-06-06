# Joomify LMS

Joomify LMS is a Joomla 6.x component package for course catalog, course delivery, enrollment, progress tracking, reporting, feature coverage auditing, and developer hooks.

## Requirements

- Joomla 6.x
- PHP 8.2 or newer
- MySQL or MariaDB supported by Joomla

## Install

1. In Joomla Administrator, open **System > Install > Extensions**.
2. Upload `pkg_joomifylms_v1.0.2.zip`.
3. Open **Components > Joomify LMS**.
4. Review **Courses**, **Lessons**, **Enrollments**, **Reports**, and **Feature Coverage**.

## Sample Data

The package includes idempotent demo data in `administrator/components/com_joomifylms/sql/sample.mysql.utf8.sql`.
Fresh installs load this sample data automatically after the schema is created, and package updates run the same seed safely without duplicating demo rows.

The demo content includes blocked sample Joomla users, LMS roles, categories, courses, curriculum modules, lessons, resources, enrollments, progress records, quizzes, assignments, certificates, badges, discussions, notifications, tenant/cohort data, payments, invoices, subscriptions, compliance records, SSO/integration placeholders, and reporting data.

Demo users are intentionally blocked and have no known password so the seed does not introduce public test logins on a client site.

## Demo URLs

- Administrator dashboard: `/administrator/index.php?option=com_joomifylms`
- Enrollments: `/administrator/index.php?option=com_joomifylms&view=enrollments`
- Reports: `/administrator/index.php?option=com_joomifylms&view=reports`
- Feature coverage: `/administrator/index.php?option=com_joomifylms&view=features`
- Frontend catalog: `/index.php?option=com_joomifylms&view=catalog`
- My Courses: `/index.php?option=com_joomifylms&view=mycourses`

## Shortcodes (Content Integration)

The package ships a content plugin (`plg_content_mtdjoomifylms`) that turns
`{joomifylms ...}` tags into live course content. It is enabled automatically on
install.

Supported tags:

| Shortcode | Result |
| --- | --- |
| `{joomifylms catalog}` | A button linking to the full course catalog. |
| `{joomifylms courses limit="3"}` | A grid of the most recent courses. |
| `{joomifylms courses category="5" type="free" limit="6"}` | Filtered grid (by category id and/or course type). |
| `{joomifylms course id="2"}` | A single course card. |

Where they work:

- **Articles / pages** — paste a shortcode directly into the article body or any
  Custom HTML module; the plugin replaces it when the content is rendered.
- **Templates / overrides** — call Joomla's content-prepare pipeline from PHP:

  ```php
  use Joomla\CMS\HTML\HTMLHelper;

  echo HTMLHelper::_('content.prepare', '{joomifylms courses limit="3"}');
  ```

All output respects the course publish state, visibility, and the current user's
view-access levels, and reuses the component stylesheet (`site.css`).

## Quality Notes

- All PHP files declare strict types.
- Joomla Web Asset Manager is used for component assets.
- User-facing strings use `MTD_JOOMIFYLMS_*` language keys.
- Database install and update SQL files are included for versions 1.0.0, 1.0.1, and 1.0.2.
- Demo seed data is deterministic and repeat-safe for installs and updates.
- Hooks are exposed through `Mtd\Component\Joomifylms\Administrator\Hooks\Manager`.
# joomifylms
