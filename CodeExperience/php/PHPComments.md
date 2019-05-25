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

require __DIR__ . '/../vendor/autoload.php';

use xx\xx;
use xx\xxx\xx;

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
     * The generation of JoJo family
	 * 
	 * Potential values are 1-7
	 *
	 * @var int
     */
    public $generation;

	/**
	 * The full name of JoJo
	 *
	 * @var string
	 */
    public $name;

    /**
	 * @var bool $stand indicates the availibility of stand power
	 * @var bool $hamon indicates the availibility of hamon energy 
     */
    public $stand, $hamon;


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
