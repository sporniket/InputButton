# InputButton
C++ library for PlatformIO, model of an input button with debouncing and event model

## LICENSE

GPL v3

## What's new

### v0.0.1

Initial publishing, extracted from working code.


## Typical application

```cpp
#include "InputButton.hpp"
// etc...

#define OK_BUTTON whatever_gpio
InputButton okButton = InputButton(OK_BUTTON) ;

void onInputButtonEvent(InputButtonEvent* event) {
    if (STATE_CHANGE == event->type && event->source->isTransient()) {
        switch (event->source->getId()) {
            case OK_BUTTON:
                if (event->source->isHigh()) {
                    // process button press...
                } else {
                    // process button release...
                }
            break;
    }
}

// interrupt to poll input pins
void onTimerInput() {
    okButton.update(digitalRead(OK_BUTTON) == HIGH)
}

void setup() {
    //...
    theButton.withDebouncer(DEBOUNCER_TYPICAL)->withListener(onInputButtonEvent) ;
    //...
    //setup timer interrupt
    //...
}



```