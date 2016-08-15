# Doctrine Delay Queue Driver Bundle

A driver for [Queue Manager Bundle](https://github.com/mcfedr/queue-manager-bundle) that uses [Doctrine](http://www.doctrine-project.org/) to store delayed jobs

This driver doesnt run jobs, it requres another driver to actually process jobs.

It currently **only** works with MySQL as a native query is required to find jobs in a concurrency safe way.

[![Latest Stable Version](https://poser.pugx.org/mcfedr/doctrine-delay-queue-driver-bundle/v/stable.png)](https://packagist.org/packages/mcfedr/doctrine-delay-queue-driver-bundle)
[![License](https://poser.pugx.org/mcfedr/doctrine-delay-queue-driver-bundle/license.png)](https://packagist.org/packages/mcfedr/doctrine-delay-queue-driver-bundle)

## Install

### Composer

    composer require mcfedr/doctrine-delay-queue-driver-bundle

### AppKernel

Include the bundle in your AppKernel

    public function registerBundles()
    {
        $bundles = [
            ...
            new Mcfedr\QueueManagerBundle\McfedrQueueManagerBundle(),
            new Mcfedr\DoctrineDelayQueueDriverBundle\McfedrDoctrineDelayQueueDriverBundle(),

## Config

With this bundle installed you can setup your queue manager config similar to this:

    mcfedr_queue_manager:
        managers:
            delay:
                driver: doctrine_delay
                options:
                    entity_manager: default
                    default_manager: default
                    default_manager_options: []

This will create a `QueueManager` service named `"mcfedr_queue_manager.delay"`

* `entity_manager` - Doctrine entity manager to use
* `default_manager` - Default job processor
* `default_manager_options` - Default options to pass to job processor `put`

## Options to `QueueManager::put`

* `time` - A `\DateTime` object of when to schedule this job
* `delay` - Number of seconds from now to schedule this job
* `manager` - Use a different job processor for this job
* `manager_options` - Options to pass to the processors `put` method

## Tables

After you have installed you will need to do a schema update so that the table of delayed tasks is created
