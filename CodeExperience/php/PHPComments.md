# Block Comment

## File Level

```php
<?php

/**
 * Short summary
 * 
 * Long description
 * 
 * @package PackageName
 * @author Moedrian
 * @copyright xxxx - xxxx Moedrian
 * @license xxxx
 * @since File availability since version xxx
 */

?>
```

## Code

```php
<?php

/**
 * Analyses JoJo Workflow
 * 
 * Description? Read those manga and animes yourself.
 *
 * @since ver 1.0
 */
class JoJo
{
    /**
     * 
     */
    public $generation;

    public $name;

    /**
     */
    public bool $stand;

    public bool $hamon;
    /**
     * Generates stand for JoJo
     *
     * Every JoJo has a stand, whether it's powerful or not.
     *
     * @param $name the name of stand
     * @param $power the power of a JoJo
     * @return $attack the stand availibility
     * @throws StandException to accept the judgement of the arrow
     * @since version 3.0
     * @see some example input for reference
     * @example the full procedure
     */
    public function stand($name, $power)
    {
        try {
            $attack = getRandom($name, $power);
        } catch (StandException $e) {
            $e->arrowStimulate();
        }
        return $attack;
    }
}

?>
```