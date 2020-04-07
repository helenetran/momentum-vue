<template lang="pug">
.weather yop
  .weather__trigger
    .weather__trigger--top
      canvas.weather-icon.meteo-btn__item(width='100')
      .temperature__current.meteo-btn__item
    .weather__trigger--bottom.location__city.meteo-btn__item
  .meteo__popup
    #meteo-city.location__city
    #meteo-state
      span.description__text ...
    div
      span.temperature__current ...
      span.temperature__feels-like(title='feels like') ...
</template>

<script>
export default {
  name: 'weather',
  data: () =>({
    city: '',
    country: ''
  }),
  mounted () {
    const axios = require("axios")

    axios({
      "method":"POST",
      "url":"https://community-neutrino-ip-info.p.rapidapi.com/ip-info",
      "headers":{
      "content-type":"application/x-www-form-urlencoded",
      "x-rapidapi-host":"community-neutrino-ip-info.p.rapidapi.com",
      "x-rapidapi-key":"75598e6402msha33bcd872cfc163p17c113jsn7df4ce859da5"
      },"data":{
      "ip":"172.20.10.2"
      }
      })
      .then((response)=>{
        console.log(response)
      })
      .catch((error)=>{
        console.log(error)
      })
// axios
    //   .get('https://ipinfo.io')
    //   .then(response => (this.getWeather(response)))
    //   .catch(() => this.getWeather())

    //   let countryCodes = {
    //     AF: 'Afghanistan', AX: 'Aland Islands', AL: 'Albania', DZ: 'Algeria', AS: 'American Samoa', AD: 'Andorra', AO: 'Angola', AI: 'Anguilla', AQ: 'Antarctica', AG: 'Antigua And Barbuda', AR: 'Argentina', AM: 'Armenia', AW: 'Aruba', AU: 'Australia', AT: 'Austria', AZ: 'Azerbaijan', BS: 'Bahamas', BH: 'Bahrain', BD: 'Bangladesh', BB: 'Barbados', BY: 'Belarus', BE: 'Belgium', BZ: 'Belize', BJ: 'Benin', BM: 'Bermuda', BT: 'Bhutan', BO: 'Bolivia', BA: 'Bosnia And Herzegovina', BW: 'Botswana', BV: 'Bouvet Island', BR: 'Brazil', IO: 'British Indian Ocean Territory', BN: 'Brunei Darussalam', BG: 'Bulgaria', BF: 'Burkina Faso', BI: 'Burundi', KH: 'Cambodia', CM: 'Cameroon', CA: 'Canada', CV: 'Cape Verde', KY: 'Cayman Islands', CF: 'Central African Republic', TD: 'Chad', CL: 'Chile', CN: 'China', CX: 'Christmas Island', CC: 'Cocos (Keeling) Islands', CO: 'Colombia', KM: 'Comoros', CG: 'Congo', CD: 'Congo, Democratic Republic', CK: 'Cook Islands', CR: 'Costa Rica', CI: 'Cote D\'Ivoire', HR: 'Croatia', CU: 'Cuba', CY: 'Cyprus', CZ: 'Czech Republic', DK: 'Denmark', DJ: 'Djibouti', DM: 'Dominica', DO: 'Dominican Republic', EC: 'Ecuador', EG: 'Egypt', SV: 'El Salvador', GQ: 'Equatorial Guinea', ER: 'Eritrea', EE: 'Estonia', ET: 'Ethiopia', FK: 'Falkland Islands (Malvinas)', FO: 'Faroe Islands', FJ: 'Fiji', FI: 'Finland', FR: 'France', GF: 'French Guiana', PF: 'French Polynesia', TF: 'French Southern Territories', GA: 'Gabon', GM: 'Gambia', GE: 'Georgia', DE: 'Germany', GH: 'Ghana', GI: 'Gibraltar', GR: 'Greece', GL: 'Greenland', GD: 'Grenada', GP: 'Guadeloupe', GU: 'Guam', GT: 'Guatemala', GG: 'Guernsey', GN: 'Guinea', GW: 'Guinea-Bissau', GY: 'Guyana', HT: 'Haiti', HM: 'Heard Island & Mcdonald Islands', VA: 'Holy See (Vatican City State)', HN: 'Honduras', HK: 'Hong Kong', HU: 'Hungary', IS: 'Iceland', IN: 'India', ID: 'Indonesia', IR: 'Iran, Islamic Republic Of', IQ: 'Iraq', IE: 'Ireland', IM: 'Isle Of Man', IL: 'Israel', IT: 'Italy', JM: 'Jamaica', JP: 'Japan', JE: 'Jersey', JO: 'Jordan', KZ: 'Kazakhstan', KE: 'Kenya', KI: 'Kiribati', KR: 'Korea', KW: 'Kuwait', KG: 'Kyrgyzstan', LA: 'Lao People\'s Democratic Republic', LV: 'Latvia', LB: 'Lebanon', LS: 'Lesotho', LR: 'Liberia', LY: 'Libyan Arab Jamahiriya', LI: 'Liechtenstein', LT: 'Lithuania', LU: 'Luxembourg', MO: 'Macao', MK: 'Macedonia', MG: 'Madagascar', MW: 'Malawi', MY: 'Malaysia', MV: 'Maldives', ML: 'Mali', MT: 'Malta', MH: 'Marshall Islands', MQ: 'Martinique', MR: 'Mauritania', MU: 'Mauritius', YT: 'Mayotte', MX: 'Mexico', FM: 'Micronesia, Federated States Of', MD: 'Moldova', MC: 'Monaco', MN: 'Mongolia', ME: 'Montenegro', MS: 'Montserrat', MA: 'Morocco', MZ: 'Mozambique', MM: 'Myanmar', NA: 'Namibia', NR: 'Nauru', NP: 'Nepal', NL: 'Netherlands', AN: 'Netherlands Antilles', NC: 'New Caledonia', NZ: 'New Zealand', NI: 'Nicaragua', NE: 'Niger', NG: 'Nigeria', NU: 'Niue', NF: 'Norfolk Island', MP: 'Northern Mariana Islands', NO: 'Norway', OM: 'Oman', PK: 'Pakistan', PW: 'Palau', PS: 'Palestinian Territory, Occupied', PA: 'Panama', PG: 'Papua New Guinea', PY: 'Paraguay', PE: 'Peru', PH: 'Philippines', PN: 'Pitcairn', PL: 'Poland', PT: 'Portugal', PR: 'Puerto Rico', QA: 'Qatar', RE: 'Reunion', RO: 'Romania', RU: 'Russian Federation', RW: 'Rwanda', BL: 'Saint Barthelemy', SH: 'Saint Helena', KN: 'Saint Kitts And Nevis', LC: 'Saint Lucia', MF: 'Saint Martin', PM: 'Saint Pierre And Miquelon', VC: 'Saint Vincent And Grenadines', WS: 'Samoa', SM: 'San Marino', ST: 'Sao Tome And Principe', SA: 'Saudi Arabia', SN: 'Senegal', RS: 'Serbia', SC: 'Seychelles', SL: 'Sierra Leone', SG: 'Singapore', SK: 'Slovakia', SI: 'Slovenia', SB: 'Solomon Islands', SO: 'Somalia', ZA: 'South Africa', GS: 'South Georgia And Sandwich Isl.', ES: 'Spain', LK: 'Sri Lanka', SD: 'Sudan', SR: 'Suriname', SJ: 'Svalbard And Jan Mayen', SZ: 'Swaziland', SE: 'Sweden', CH: 'Switzerland', SY: 'Syrian Arab Republic', TW: 'Taiwan', TJ: 'Tajikistan', TZ: 'Tanzania', TH: 'Thailand', TL: 'Timor-Leste', TG: 'Togo', TK: 'Tokelau', TO: 'Tonga', TT: 'Trinidad And Tobago', TN: 'Tunisia', TR: 'Turkey', TM: 'Turkmenistan', TC: 'Turks And Caicos Islands', TV: 'Tuvalu', UG: 'Uganda', UA: 'Ukraine', AE: 'United Arab Emirates', GB: 'United Kingdom', US: 'United States', UM: 'United States Outlying Islands', UY: 'Uruguay', UZ: 'Uzbekistan', VU: 'Vanuatu', VE: 'Venezuela', VN: 'Viet Nam', VG: 'Virgin Islands, British', VI: 'Virgin Islands, U.S.', WF: 'Wallis And Futuna', EH: 'Western Sahara', YE: 'Yemen', ZM: 'Zambia', ZW: 'Zimbabwe'
    //   }
    //   let country =  countryCodes[location.country]
    //   this.city = location.city
    //   this.country = country
  },
  methods: {
    // Get location using https://ipinfo.io .
      // axios
      // .get('https://quotes.rest/qod')
      // .then(response => (this.getQuoteOfTheDay(response)))
      // .catch(() => {this.getQuoteOfTheDay()})

    // Get weather using https://dark-sky.p.rapidapi.com.
    getWeather (loc) {
      console.log('get weather to be done', 'loc = ', loc)
      // Get local weather.
      // const url = 'https://dark-sky.p.rapidapi.com/'+loc+'?lang=en&units=auto'
      // const settings = {
      //   'async': true,
      //   'crossDomain': true,
      //   'url': url,
      //   'method': 'GET',
      //   'headers': {
      //     'x-rapidapi-host': 'dark-sky.p.rapidapi.com',
      //     'x-rapidapi-key': '75598e6402msha33bcd872cfc163p17c113jsn7df4ce859da5'
      //   }
      // }

      // axios(settings).done(function(weather) {
      //   let tempFeelsLike = Math.round(weather.currently.apparentTemperature)
      //   let tempCurrent = Math.round(weather.currently.temperature)
      //   let weatherIcon = weather.currently.icon
      //   let weatherSummary = weather.currently.summary

      //   $('.temperature__current').html(tempCurrent + '°');
      //   $('.temperature__feels-like').html(tempFeelsLike + '°');
      //   $('.weather-icon').attr('id', `${weatherIcon}`);
      //   $('.description__text').html(weatherSummary);
      //   loadIcons()
      // });

      // Get icon Canvas.
      // loadIcons () {
      //   let newSkycons = new Skycons({'color': '#fff'});
      //   let skycons1, skycons2, skycons3, skycons4, skycons5, skycons6, skycons7, skycons8, skycons9, skycons10
      //   let skycons = [skycons1, skycons2, skycons3, skycons4, skycons5, skycons6, skycons7, skycons8, skycons9, skycons10]
      //   let skyconsClasses = ['clear-day', 'clear-night', 'rain', 'snow', 'wind', 'sleet', 'fog', 'cloudy', 'partly-cloudy-day', 'partly-cloudy-night']
      //   let skyconsIcons = [Skycons.CLEAR_DAY, Skycons.CLEAR_NIGHT, Skycons.RAIN, Skycons.SNOW, Skycons.WIND, Skycons.SLEET, Skycons.FOG, Skycons.CLOUDY, Skycons.PARTLY_CLOUDY_DAY, Skycons.PARTLY_CLOUDY_NIGHT]

      //   for (i = 0; i < 10; i++) skycons[i] = newSkycons
      //   for (j = 0; j < 10; j++) skycons[j].add(skyconsClasses[j], skyconsIcons[j])
      //   for (k = 0; k < 10; k++) skycons[k].play()
      // }
    }
  }
}
</script>

<style lang="scss">
.weather {
	position: fixed;
	// top: -4%;
	right: 2%;
	opacity: 0.8;
}

.weather__trigger {cursor: pointer;}

.weather__trigger--top {
	display: flex;
	justify-content: space-around;
}

.weather__trigger--top .temperature__current	{
	position: absolute;
	top: 51px;
	left: 49px;
	font-size: 22px;
}

.weather__trigger--bottom	{
	text-align: center;
	font-size: 13px;
}

#temperature {
	font-size: 1.9em;
	opacity: 1;
	position: relative;
  top: 10%;
  right: -6%;
  text-align: center;
  font-family: arial;
  opacity: 1;
  cursor: pointer;
}

#location {
  position: relative;
  top: 20%;
  right: -6%;
  text-align: center;
  font-size: 0.85em;
  padding-top: 5px;
  opacity: 0.7;
	cursor: pointer;
}

.meteo__popup {
	width: 362px;
	height: 181px;
	background-color: black;
	position: fixed;
	right: 1.45%;
	top: 12%;
	border-radius: 5px;
	padding: 19px;
	font-size: 1.3em;
	opacity: 0;
	transition: 0.3s ease-in-out;
	text-align: center;
	z-index: -50;
}

.meteo__popup .temperature__feels-like {opacity: 0.5;}

.meteo__popup:before {
  content: "";
  width: 0;
  height: 0;
  border: 7px solid transparent;
  border-bottom-color: black;
  opacity: 0.9;
  position: absolute;
  right: 12.5%;
  bottom: 100%;
}

#meteo-city {font-size: 1.2em;}

#meteo-state {
	opacity: 0.8;
	font-size: 1.1em;
	margin-bottom: 10px;
}

#meteo-icon {
	font-size: 3.5em;
	font-style: normal;
	color: white;
	opacity: 1;
}
</style>

