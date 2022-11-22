# XBOX Logo

This is an animated logo for XBOX. I designed it to fill the center 'x' to fill with green. When turned on, there is a 'glow' that happens.

Designed by LilTrublMakr

## Preview

| Turning On | On | Turning Off | Off |
| --- | --- | --- | --- |
| ![Turning On](./turning-on.svg) | ![On](./on.svg) | ![Turning Off](./turning-off.svg) | ![Off](./off.svg) |

## icons.yaml

```yaml
icon_xbox:
  template:
    - base
    - loader
  styles:
    custom_fields:
      icon:
        - width: 79%
        - pointer-events: none
        - display: grid
        - margin-left: -10%
        - fill: >
            [[[
              return (variables.state === 'on' || variables.state === 'playing') ? '#9da0a2' : '#9da0a2';
            ]]]
  custom_fields:
    icon: >
      [[[
        let style = `
          <style>
            .glow {
              stroke: #9da0a2;
              opacity: 0;
              animation: glow 1s ease-out;
              animation-delay: 1s;
            }

            .inner {
              fill: #107B10;
            }
          
            .inner-on {
              animation: inner-on 1s linear;
              animation-fill-mode: both;
              transform-origin: center center;
            }

            .inner-off {
              animation: inner-off 1s linear backwards;
              animation-fill-mode: both;
              transform-origin: center center;
            }
          
            @keyframes glow {
              from {
                opacity: 1;
                stroke-width: 0;
              }
              to {
                opacity: 0;
                stroke-width: 4px;
              }
            }
          
            @keyframes inner-on {
              from {
                transform: scale(0);
              }
              to {
                transform: scale(1);
              }
            }
          
            @keyframes inner-off {
              from {
                transform: scale(1);
              }
              to {
                transform: scale(0);
              }
            }
          </style>
        `;
        let state;
        if (variables.state === 'on' && variables.timeout < 2000) {
          state = `
            <circle class="glow" cx="50%" cy="50%" r="10"/>
            <circle class="inner inner-on" cx="50%" cy="50%" r="10" />
          `;
        } 
        if (variables.state === 'off' && variables.timeout < 2000) {
          state = `
            <circle class="inner inner-off" cx="50%" cy="50%" r="10" />
          `;
        }
        if (variables.state === 'on' && variables.timeout > 2000) {
          state = `
            <circle class="inner" cx="50%" cy="50%" r="10" />
          `;
        }
        return `
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="40">
            ${style}
            ${state}
            <path d="M5,4.9L5,4.9L5,4.9C3.1,6.8,2,9.3,2,12c0,2.2,0.7,4.3,2,6.1c0,0,0,0,0.1,0c0,0,0,0,0-0.1 C3.3,15.7,7.2,10,9.3,7.6c0,0,0,0,0,0c0,0,0,0,0,0C5.9,4.1,5,4.9,5,4.9 M19,4.9L19,4.9L19,4.9c1.9,1.9,3,4.4,3,7.1 c0,2.2-0.7,4.3-2,6.1c0,0,0,0-0.1,0c0,0,0,0,0-0.1c0.8-2.4-3.1-8.1-5.1-10.5c0,0,0,0,0,0c0,0,0,0,0,0C18.1,4.1,19,4.9,19,4.9 M12,2 c2,0,3.7,0.6,5.2,1.5c0,0,0,0,0,0c0,0,0,0,0,0C15.2,3.1,12.3,4.8,12,5c0,0,0,0,0,0c0,0,0,0,0,0c-0.7-0.4-3.5-1.8-5.2-1.4 c0,0,0,0,0,0c0,0,0,0,0,0C8.3,2.6,10,2,12,2 M12,10C12,10,12,10,12,10c3,2.3,8.1,7.9,6.6,9.5l0,0l0,0h0C16.8,21.1,14.4,22,12,22 c-2.4,0-4.8-0.9-6.6-2.5l0,0l0,0C3.9,17.9,9,12.3,12,10C12,10,12,10,12,10"/>
          </svg>
        `;
      ]]]
```