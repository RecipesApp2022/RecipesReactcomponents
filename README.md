# 🚀 Frontend - Perfil del cliente

 
## Índice de contenidos
* [AppLayout](#item1)
	 * [NavBar](#item2)
	 * [NavInfo](#item3)
	 * [Footer](#item4)
* [LoginForm](#item5)
* [RegisterForm](#item6)
* [SwiperHome](#item7)
* [Card](#item8)
* [CategorySectionCard](#item9)
* [PopularSearch](#item10)
* [SwiperWeightPlan](#item11)
* [CategoriesVideo](#item12)
	* [SesionCategory](#item13)
	* [VideoCategory](#item14)
	* [Video](#item15)
* [Recipes](#item16)
* [ChefsCountries](#item17)
* [AuthModal](#item18)
* [ButtonSupr](#item19)
* [MenuLeft](#item20)
* [CategoriesRecipes](#item21)
* [SelectCategory](#item22)
* [SelectRank](#item23)
* [ButtonRank](#item24)
* [BannerChef](#item25)
* [ButtomButton](#item26)
* [ProductImagenCarousel](#item27)
* [Matches](#item28)
* [MenuConfig](#item29)
* [MyAccountLayout](#item30)
* [PageLogo](#item31)
* [NavSearchBar](#item32)
* [CertificationChef](#item33)
* [Post](#item34)
* [DescriptionChef](#item35)
* [ButtonImage](#item36)
* [Details](#item37)
* [](#item38)
* [Tab](#item39)
* [TabButton](#item40)
* [TabPanel](#item41)
* [TabsContainer](#item42)
* [TotalShopping](#item43)
* [TotalShoppingPrice](#item44)
* [InformationChef](#item45)
* [DescriptionPost](#item46)
* [CalendarDay](#item47)
* [calendar](#item48)
* [RequireAuth](#item49)
* [ScrollNavegacion](#item50)
* [SearchHome](#item51)
* [ButtonSearch](#item52)
* [WeightPlan](#item53)
* [Swiper](#item54)
* [config](#item55)
* [DescriptionChef](#item56)
* [DescriptionPost](#item57)
* [FormAccount](#item58)
* [InformacionChef](#item59)
* [ingredientRow](#item60)
* [ingredientRowDetails](#item61)
* [LyOverview](#item62)
* [MealDetailOverview](#item63)
* [MealDetailOverviewImages](#item64)
* [PasswordUser](#item65)
* [PaypalLogin](#item66)
* [PaypalUser](#item67)
* [ProductInfo](#item68)
* [BannerPage](#item69)
* [BoxCalendar](#item70)
* [BoxName](#item71)
* [ButtonCart](#item72)
* [ButtonChange](#item73)
* [ButtonItems](#item74)
* [SelectOrder](#item75)
* [CardChef](#item76)
* [CardGym](#item77)
* [CardOrder](#item78)
* [CardPaypal](#item79)
* [CardProduct](#item80)
* [Card Recipes](#item81)
* [CardResum](#item82)
* [CardWithTitle](#item83)
* [Checkbox](#item84)
* [CheckboxConfig](#item85)
* [WaPay](#item86)



<a name="item1"></a>
### AppLayout
 ---
Es el componente padre de enrutamiento entre los hijos NavBar, NavInfo y Footer. 

Este recibe por parametro {children} que permite agregar el contenido o cuerpo  correspondiente a cada página de la aplicación con la estructura ya definida de sus componentes hijos. 

#### Código: 

Importación de la libreria useEffect, los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente.

Importación de la libreria react-router-dom Consulte la guía de inicio para obtener más información sobre cómo comenzar con El paquete react-router-dom contiene enlaces para usar React Router en aplicaciones web. 

Importación de la libreria Footer, NavBar, NavInfo son componente para una función en particular.

```
import { useEffect } from "react";
import { useLocation } from "react-router-dom";
import Footer from "./Footer";
import NavBar from "./NavBar";
import NavInfo from "./NavInfo";
const AppLayout = ({ children }) => {
    const location = useLocation();
    useEffect(() => {
        window.scrollTo({ top: 0 });
    }, [location]);
    return (
        <div className="bg-gray-100">
            <NavBar />
            <NavInfo />
            {children}
            <Footer />
        </div>
    	)
    }export default AppLayout;
```

La compilación del código es el diseño de la unión de 3 componente para la construcción de otras posibles vista en nuestro sistema web.

![](https://i.imgur.com/pikOfoH.png)

[Subir](#top)

<a name="item2"></a>
* ### NavBar
 ---
Contiene la parte superior del header donde se ubican los items que direccionan la navegación del usuario hacia categorías, vendedores, notificación e inicio de sesión. 

No recibe ningun parámetro. 

Importación de la líbreria react-icons que utiliza importaciones de ES6 que le permiten incluir solo los íconos que usa su proyecto.

Implementación de la líbreria en este es un caso de uso perfecto para un useAuthgancho que habilita cualquier componente. para obtener el estado de autenticación actual y volver a renderizar si cambia. 

Importación de la libreria useEffect, los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente.


#### Código
```
import PageLogo from "./PageLogo";
import React, { useEffect, useState } from 'react'
import { FaUserCircle } from "react-icons/fa";
import { BsBell } from "react-icons/bs";
import { BiSearchAlt } from "react-icons/bi";
import AuthModal from "./AuthModal";
import { Link, useLocation, useSearchParams } from "react-router-dom";
import { useAuth } from "../contexts/AuthContext";
import MenuConfig from "./MenuConfig";
import MobileMenuButton from "./MobileMenuButton";
import clsx from "clsx";
import MovilMenuSearch from "./MovilMenuSearch";
import NotificationComponent from "./Notifications/NotificationComponent";

const NavBar = () => {
    
    const { user } = useAuth();

    const [searchParams] = useSearchParams();

    const [showModal, setShowModal] = useState(false);

    const [showModalMenu, setShowModalMenu] = useState(false);

    const [showMenu, setShowMenu] = useState(false);

    const [currentPath, setCurrentPath] = useState(""); //pat escucha 
    useEffect(() => {
        setShowModal(searchParams?.get('showLogin'));
    }, [searchParams])
    const handleToggleModal = () => {
        setShowModal((oldShowModal) => !oldShowModal);
        return;
    }
    const handleToggleMenu = () => {
        setShowMenu((oldShowMenu) => !oldShowMenu);
    }
    const location = useLocation();
    useEffect(() => {
        setCurrentPath(location?.pathname);
    }, [location]);
    return (
        <>
            <div className="bg-gray-800 text-white h-14 px-4">
                <div className="container h-full">
                    <div className="flex md:justify-none items-center h-full text-base">
                        <PageLogo />
                        {/* <NavSearchBar /> */}
                        <div className="flex ml-auto md:space-x-10 space-x-8 items-center h-full" >
                            <Link to={"/Categories"} className="hidden md:block hover:text-main">
                                <p className={clsx({
                                    "text-main title-medium md:text-lg": currentPath === '/Categories',
                                    'text-white title-medium md:text-lg': currentPath !== '/Categories'
                                })}>
                                    Categories
                                </p>
                            </Link>
                            <Link to={"/Sellers"} className="hidden md:block hover:text-main">
                                <p className={clsx({
                                    "text-main title-medium md:text-lg": currentPath === '/Sellers',
                                    'text-white title-medium md:text-lg': currentPath !== '/Sellers'
                                })}>
                                    Sellers
                                </p>
                            </Link>
                            {
                                user &&
                                <NotificationComponent />
                            }
                            <button
                                className="md:hidden hover:text-main"
                                onClick={() => setShowModalMenu(true)}
                            >
                                <BiSearchAlt className="h-6 w-6 md:ml-10" />
                            </button>
                            <button onClick={user ? handleToggleMenu : handleToggleModal} className="hidden md:block relative items-center hover:text-main bg-transparent 
                                    bg-gray-800 border border-slate-300 hover:border-main rounded-md py-2 px-2.5">
                                <div className="flex text-lg">
                                    <FaUserCircle className="m-auto mr-2" />
                                    {user ? user.name : 'Log in'}
                                    <MenuConfig show={showMenu} onClose={() => setShowMenu(false)} />
                                </div>

                            </button>
                            <MobileMenuButton />
                        </div>
                    </div>
                </div>
            </div>
            <AuthModal show={showModal} onClose={handleToggleModal} />
            <MovilMenuSearch show={showModalMenu} onClose={() => setShowModalMenu(false)} />
        </>
    );
    }export default NavBar;
```
Cómo resultado de la ejecución de código es:

![](https://i.imgur.com/5uM6FpB.png)

[Subir](#top)

<a name="item3"></a>
* ### NavInfo
 ---
Contiene la barra inferior del header, está compuesto por la localización, direccionamientos hacia recetas, planes y combos.

Cómo parámetro no recibe nada.

Importación de la líbreria react-icons que utiliza importaciones de ES6 que le permiten incluir solo los íconos que usa su proyecto.

Importación de la libreria react-router-dom Consulte la guía de inicio para obtener más información sobre cómo comenzar con El paquete react-router-dom contiene enlaces para usar React Router en aplicaciones web. 

Importación de la libreria useEffect, los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente.

Importación de la líbreria useState es un React Hook que le permite agregar una variable de estado a su componente.

#### Código
```
import { BiMap } from "react-icons/bi";

import { Link, useLocation } from "react-router-dom";

import { useEffect, useState } from "react";

import clsx from "clsx";

const NavInfo = () => {
    const [currentPath, setCurrentPath] = useState(""); //pat escucha 
    const location = useLocation();
    useEffect(() => {
        setCurrentPath(location?.pathname);
    }, [location]);
    return (
        <div className="bg-main text-black py-1">
            <div className="relative flex items-center justify-center">
                <BiMap className="text-white text-xl absolute left-5" />
                <div className="flex items-center justify-center flex-wrap">
                    <nav className="flex items-center space-x-10  md:space-x-20">
                        <Link to={"/recipes"}>
                            <p className={clsx("hover:text-white", {
                                "text-white title-medium md:text-lg": currentPath === '/recipes',
                                "text-black title-medium md:text-lg": currentPath !== '/recipes'
                            })}>
                                Recipes
                            </p>
                        </Link>

                        <Link to={"/plans"}>
                            <p className={clsx("hover:text-white", {
                                "text-white title-medium md:text-lg": currentPath === '/plans',
                                "text-black title-medium md:text-lg": currentPath !== '/plans'
                            })}>
                                Plans
                            </p>
                        </Link>
                        <Link to={"/combos"}>
                            <p className={clsx("hover:text-white", {
                                "text-white title-medium md:text-lg": currentPath === '/combos',
                                "text-black title-medium md:text-lg": currentPath !== '/combos'
                            })}>
                                Combos</p>
                        </Link>
                    </nav>
                </div>
            </div>
        </div >
    );
    }export default NavInfo;
```
![](https://i.imgur.com/hP1OO0n.png)

[Subir](#top)

 
<a name="item4"></a>
* ### Footer
 ---
Almacena toda la información del pié de página y no es necesario que reciba ningun parámetro ya que el componente consiste en el diseño del footer.

Cómo parémetro no recibe nada.

#### Código

```
import React from "react";
import PageLogo from "./PageLogo";
import { SiFacebook } from "react-icons/si";
import { SiInstagram } from "react-icons/si";
import { SiTwitter } from "react-icons/si";
import { IoLogoYoutube } from "react-icons/io";
import { FaLinkedinIn } from "react-icons/fa";

export default function Footer() {
  return (
    <footer className="bg-gray-900 text-white mt-auto p-5 md:m-auto">
      <div className="container h-full">
        <div className="flex items-center justify-center mb:ml-8 mt-4 md:justify-start">
          <PageLogo />
          <b className="ml-4 title-medium">Ricardo APP</b>
        </div>
        <ul className="grid grid-cols-2 gap-8 p-6 md:px-28  md:grid-cols-4 md:mt-4 ">
          <li>
            <h1 className="font-bold my-4">
              Get in touch
            </h1>
            <ul>
              <li className="md:my-4">About Us</li>
              <li className="md:my-4">Careers</li>
              <li className="md:my-4">Press Releases</li>
              <li className="md:my-4">Blog</li>
            </ul>
          </li>
          <li>
            <h1 className="font-bold my-4">Connections</h1>
            <ul className="">
              <li className="space-x-2 flex md:mt-4 md:mb-4">
                <SiFacebook className="md:h-6 md:w-6 h-4 w-4 mt-1 cursor-pointer hover:text-main md:cursor-pointer mr-1" />
                Facebook
              </li>
              <li className="space-x-2 flex md:mt-4 md:mb-4">
                <SiTwitter className="md:h-6 md:w-6 h-4 w-4 mt-1 cursor-pointer hover:text-main md:cursor-pointer mr-1" />
                Twitter
              </li>
              <li className="space-x-2 flex md:mt-4 md:mb-4">
                <SiInstagram className="md:h-6 md:w-6 h-4 w-4 mt-1 cursor-pointer hover:text-main md:cursor-pointer mr-1" />
                Instagram
              </li>
              <li className="space-x-2 flex md:mt-4 md:mb-4">
                <IoLogoYoutube className="md:h-6 md:w-6 h-4 w-4 mt-1 cursor-pointer hover:text-main md:cursor-pointer mr-1" />
                Youtube
              </li>
              <li className="space-x-2 flex md:mt-4 md:mb-4">
                <FaLinkedinIn className="md:h-6 md:w-6 h-4 w-4 mt-1 cursor-pointer hover:text-main md:cursor-pointer mr-1" />
                LinkedinIn
              </li>
            </ul>
          </li>
          <li>
            <h1 className="font-bold my-4">
              Earnings
            </h1>
            <ul>
              <li className="md:my-4">Become an Affiliate</li>
              <li className="md:my-4">Advertise your product</li>
              <li className="md:my-4">Sell on Market</li>
            </ul>
          </li>
          <li>
            <h1 className="font-bold my-4">
              Account
            </h1>
            <ul>
              <li className="md:my-4">Your account</li>
              <li className="md:my-4">Returns Centre</li>
              <li className="md:my-4">100 % purchase protection</li>
              <li className="md:my-4">Chat with us</li>
              <li className="md:my-4">Help</li>
            </ul>
          </li>
        </ul>
      </div>
      <div className="text-center mt-10 ">
        <p>&copy; 2022 <span className='text-main'>Ricardo APP.</span> All rights reserved. Designed by JV, AN, LV & FJ.</p>
      </div>
    </footer >
  );
}
```
    
![](https://i.imgur.com/69B1bHz.png) 

[Subir](#top)

<a name="item5"></a>
### LoginForm
 ---
La vista del login donde el usuario agrega datos para validar su acceso a la plataforma.

Recibe como parámetro { changeForm, onClose } changeForm, lo que hace es avisar al componente padre en que modal estoy y onClose me permite cerrar el modal donde se encuentre.

Importación de la libreria useEffect, los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente.

Importación de la líbreria useState es un React Hook que le permite agregar una variable de estado a su componente.

Importación de la líbreria useAxios es un cliente HTTP basado en promesasnode.js para el navegador. Es isomorfo (= puede ejecutarse en el navegador y nodejs con la misma base de código). En el lado del servidor usa el httpmódulo nativo node.js, mientras que en el cliente (navegador) usa XMLHttpRequests.

#### Código
```
import { useEffect, useState } from "react";
import Logo from "../assets/drafts.png";
import LoginBg from "../assets/img1.jpg";
import PageLogo from "../componentes/PageLogo";
import { useAuth } from "../contexts/AuthContext";
import { useFeedBack } from "../contexts/FeedBackContext";
import useAxios from "../hooks/useAxios";
import Checkbox from "./Checkbox";
const LoginForm = ({ changeForm, onClose }) => {
    const { setAuthInfo } = useAuth();
    const { setLoading } = useFeedBack();
    const [formData, setFormData] = useState({ email: '', password: '' });
    const [{ data: loginData, loading: loginLoading }, login] = useAxios({ url: '/auth/login', method: 'POST' }, { manual: true, useCache: false });
    useEffect(() => {
        setLoading({
            show: loginLoading,
            message: 'Login'
        })
    }, [loginLoading]);
    useEffect(() => {
        if (loginData) {
            setAuthInfo({
                user: loginData?.user,
                token: loginData?.accessToken
            });
            onClose(null, true);
        }
    }, [loginData])
    const handleChange = (e) => {
        setFormData(prevData => ({
            ...prevData,
            [e.target.name]: e.target.value,
        }));
    }
    const handleSubmit = (e) => {
        e.preventDefault();

        login({ data: formData });
    }
    return (
        <div className="m-auto grid md:grid-cols-2 md:w-2/3 bg-main animate__animated animate__fadeInUp">
            <div style={{ backgroundImage: `url(${LoginBg})`, backgroundPosition: 'center center', backgroundSize: 'cover' }}>
                <div className="flex h-full w-full bg-black bg-opacity-50 p-4">
                    <div className="m-auto" >
                        <img src={Logo} className="m-auto rounded-2xl" alt="RicardoApp" />
                        <h1 className="text-4xl text-center text-white font-bold">Ricardo App</h1>
                        <p className="font-light text-sm text-center text-white">the best platform to grow your Recipes.</p>
                    </div>
                </div>
            </div>
            <form onSubmit={handleSubmit} className="p-4">
                <div className="text-center">
                    <PageLogo centered />
                    <h1 className="mt-4 text-2xl text-white font-bold">Login</h1>
                    <div className="mx-1 my-2 h-px w-0.2 bg-white"></div>
                </div>
                <div className="text-white ">
                    <p className="font-bold mt-4">E-Mail Address</p>
                    <input
                        className="border border-slate-100 rounded-md py-2 px-2 w-full text-black"
                        placeholder="Email"
                        type="email"
                        name="email"
                        value={formData?.email}
                        onChange={handleChange}
                    />
                    <p className="font-bold">Password</p>
                    <input
                        className="border border-slate-100 rounded-md py-2 px-2 w-full text-black"
                        placeholder="Password"
                        type="password"
                        name="password"
                        value={formData?.password}
                        onChange={handleChange}
                    />
                </div>
                <div className="flex mx-2 my-2 ">
                    <Checkbox className="mt-1.5" />
                    <p className="text-white ml-2" >remember me</p>
                </div>
                <div className="text-center">
                    <button className="bg-slate-50 px-2 py-1 rounded">sing in</button>
                    <div className="px-2 py-1 mb-2 text-white">
                        <p onClick={() => changeForm('forgot-password')} className="mb-2 cursor-pointer">I forgot my password?</p>
                        <p className="mb-2">You do not have an account?
                            <b className="cursor-pointer text-slate-700" onClick={() => { changeForm('register') }}> Sign up</b>
                        </p>
                        <div className=" mb-2 text-center">
                            <p>&copy; 2022 <b className='text-white'>Ricardo APP.</b> All rights reserved. Designed by JV, AN, LV & FJ</p>
                        </div>
                    </div>
                </div>
            </form>
        </div>
    )
}export default LoginForm;
```
Cómo ejecución el resultado obtenido del código es lo que se visualiza en la imagen.

![](https://i.imgur.com/hWaV5bx.png)

[Subir](#top)

<a name="item6"></a>
### RegisterForm
 ---
Página en la cual el usuario puede rellenar los campos requeridos para el registro en la aplicación.

Recibe como parámetro { changeForm, onClose }, changeForm lo que hace es avisar al componente padre en que modal estoy y onClose me permite cerrar el modal donde se encuentre.

Importación de la libreria useEffect, los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente.

Importación de la líbreria useState es un React Hook que le permite agregar una variable de estado a su componente.

Importación de la líbreria useAxios es un cliente HTTP basado en promesasnode.js para el navegador. Es isomorfo (= puede ejecutarse en el navegador y nodejs con la misma base de código). En el lado del servidor usa el httpmódulo nativo node.js, mientras que en el cliente (navegador) usa XMLHttpRequests.

Importación de la libreria react-router-dom Consulte la guía de inicio para obtener más información sobre cómo comenzar con El paquete react-router-dom contiene enlaces para usar React Router en aplicaciones web.

#### Código
```
import { useEffect, useState } from "react";
import Logo from "../assets/drafts.png";
import LoginBg from "../assets/img1.jpg";
import PageLogo from "../componentes/PageLogo";
import { useAuth } from "../contexts/AuthContext";
import useAxios from "../hooks/useAxios";
import { useNavigate } from 'react-router-dom';
const RegisterForm = ({ changeForm, onClose }) => {
    const navigate = useNavigate();
    const { setAuthInfo } = useAuth();
    const [data, setData] = useState({
        name: "",
        email: "",
        phoneNumber: "",
        password: "",
        passwordVerification: "",
        instagram: '',
        paypal: ''
    });
    const [{ data: registerData, loading: registerLoading }, register] = useAxios({ url: `/auth/register`, method: 'POST' }, { manual: true, useCache: false });
    useEffect(() => {
        if (registerData) {
            setAuthInfo({
                user: registerData?.user,
                token: registerData?.accessToken
            });
            onClose(null, true);
            navigate('/accountinfo');
        }
    }, [registerData])

    const handleChange = (e) => {
        setData((oldData) => {
            return {
                ...oldData,
                [e.target.name]: e.target.value
            }
        });
    }
    const handleSubmit = (e) => {
        e?.preventDefault?.();
        if (registerLoading) return;
        if (data?.password !== data.passwordVerification) {
            alert('Las contraseñas no coinciden.');
            return;
        }
        const { passwordVerification, ...rest } = data;
        register({ data: rest });
    }
    return (
        <div className="m-auto grid md:grid-cols-2 bg-main animate__animated animate__fadeInUp">
            <div style={{ backgroundImage: `url(${LoginBg})`, backgroundPosition: 'center center', backgroundSize: 'cover' }}>
                <div className="flex h-full w-full bg-black bg-opacity-50 p-4">
                    <div className="m-auto" >
                        <img src={Logo} className="m-auto rounded-2xl" alt="RicardoApp" />
                        <h1 className="text-4xl text-center text-white font-bold">Ricardo App</h1>
                        <p className="font-light text-sm text-center text-white">the best platform to grow your Recipes.</p>
                    </div>
                </div>
            </div>
            <form onSubmit={handleSubmit} className="p-4 custom-scrollbar custom-scrollbar-light" style={{ maxHeight: '80vh', overflowY: 'auto' }}>
                <div className="text-center">
                    <PageLogo centered />
                    <h1 className="mt-4 text-2xl text-white font-bold">Registration</h1>
                    <div className="mx-1 my-2 h-px w-0.2 bg-white"></div>
                </div>
                <div className="mt-2 grid md:grid-cols-2 text-white ">
                    <div className="mx-2 my-2">
                        <span className="font-bold">Name and Surname:</span>
                        <input
                            className="border border-slate-100 rounded-md py-2 px-2 w-full text-black"
                            placeholder="Name"
                            type="text"
                            name="name"
                            value={data?.name}
                            onChange={handleChange}
                        />
                    </div>
                    <div className="mx-2 my-2">
                        <span className="font-bold">E-Mail Address</span>
                        <input
                            className="border border-slate-100 rounded-md py-2 px-2 w-full text-black"
                            placeholder="email"
                            type="email"
                            name="email"
                            value={data?.email}
                            onChange={handleChange}
                        />

                    </div>
                    <div className="mx-2 my-2">
                        <span className="font-bold">Password</span>
                        <input
                            className="border border-slate-100 rounded-md py-2 px-2 w-full text-black"
                            placeholder="Password"
                            type="password"
                            name="password"
                            value={data?.password}
                            onChange={handleChange}
                        />
                    </div>
                    <div className="mx-2 my-2">
                        <span className="font-bold">Confirm Password:</span>
                        <input
                            className="border border-slate-100 rounded-md py-2 px-2 w-full text-black"
                            placeholder="Confirm Password"
                            type="password"
                            name="passwordVerification"
                            value={data?.passwordVerification}
                            onChange={handleChange}
                        />
                    </div>
                    <div className="mx-2 my-2">
                        <span className="font-bold">Contact number and WhatsApp:</span>
                        <input
                            className="border border-slate-100 rounded-md py-2 px-2 w-full text-black"
                            placeholder="+ 000 000 00000000"
                            type="text"
                            name="phoneNumber"
                            value={data?.phoneNumber}
                            onChange={handleChange}
                        />
                    </div>
                    <div className="mx-2 my-2">
                        <p className="font-bold">User Instagram:</p>
                        <input className="border border-slate-100 rounded-m py-2 px-2 w-full text-black"
                            placeholder="@xxxxxxxxxxxx" type="text" name="instagram" value={data?.instagram} onChange={handleChange}/>
                    </div>
                    <div className="mx-2 my-2">
                        <p className="font-bold">User PayPal:</p>
                        <input className="border border-slate-100 rounded-md py-2 px-2 w-full text-black"
                            placeholder="xxxxx@xxxx.xxx" type="email" name="paypal" value={data?.paypal} onChange={handleChange}/>
                    </div>
                </div>
                <div className="text-center">
                    <button className="bg-slate-50 px-2 py-1 rounded" disabled={registerLoading}>
                        {
                            registerLoading ?
                                'Loading...'
                                :
                                'Sing in'
                        }
                    </button>
                    <div className="px-2 py-1 mb-2 text-white">
                        <p className="mb-2">You do not have an account? <b className="cursor-pointer text-slate-700" onClick={() => { changeForm('login') }}>Sign in</b></p>
                        <div className=" mb-2 text-center">
                            <p>&copy; 2022 <b className='text-white'>Ricardo APP.</b> All rights reserved. Designed by JV, AN, LV & FJ</p>
                        </div>
                    </div>
                </div>
            </form>
        </div >
    )
}export default RegisterForm;
```
![](https://i.imgur.com/T8lMgYk.png)

[Subir](#top)

<a name="item7"></a>
### SwiperHome
 ---
Contiene las imágenes de portada modo slider, este componente no recibe parámetros. 

Cómo parámetro no recibe nada.

Importación de la libreria useEffect, los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente.

Importación de la líbreria useState es un React Hook que le permite agregar una variable de estado a su componente.

#### Código
```
import React, { useState, useEffect } from "react";
import { Swiper, SwiperSlide } from "swiper/react";// Import Swiper React components
import img1 from "../assets/img1.jpg";
import img2 from "../assets/img2.jpg";
import img3 from "../assets/img3.jpg";
import { Pagination, Navigation } from "swiper";
import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";
import SearchHome from "../componentes/SearchHome";
const SwiperHome = () => {
    const [innerWidth, setInnerWidth] = useState(window.innerWidth);
    useEffect(() => {
        const resizeHandler = () => {
            setInnerWidth(window.innerWidth);
        };
        window.addEventListener('resize', resizeHandler);
        return () => window.removeEventListener('resize', resizeHandler);
    }, []);
    return (
        <div className='relative'>
            <Swiper
                slidesPerView={innerWidth > 768 ? 1 : 1}
                spaceBetween={30}
                loop={true}
                pagination={{ clickable: true, }}
                navigation={true}
                style={{ padding: innerWidth > 768 ? '0' : 10 }}
                modules={[Pagination, Navigation]}
                className="mySwiper">
                <SwiperSlide>
                    <img className="w-full h-40 md:h-72" src={img1} alt="img1" />
                </SwiperSlide>
                <SwiperSlide>
                    <img className="w-full h-40 md:h-72" src={img2} alt="img2" />
                </SwiperSlide>
                <SwiperSlide>
                    <img className="w-full h-40 md:h-72" src={img3} alt="imh3" />
                </SwiperSlide>
            </Swiper>
            <SearchHome />
        </div>
    );
}export default SwiperHome; 
```
Cómo ejecución el resultado obtenido del código es lo que se visualiza en la imagen, Sólo se encarga de mostrar la imagen del banner.

![](https://i.imgur.com/Glk2nCD.jpg) 

[Subir](#top)

<a name="item8"></a>
### Card
 ---
Titulación de las secciones. Recibe parámetro de texto modificable, debido a que se utiliza en varias secciones del home.

Cómo parámetros recibe una variable llamada props que es la encargada del nombre que se mostrará en el resultado de la ejecución del componente en la plataforma.

Importación de la libreria react-router-dom Consulte la guía de inicio para obtener más información sobre cómo comenzar con El paquete react-router-dom contiene enlaces para usar React Router en aplicaciones web. 

#### Código
```
import React, { Fragment } from "react";
import { Link } from "react-router-dom";
const Card = (props) => {
  return (
    <Fragment>
      <div className="relative flex justify-center text-center md:h-14 cursor-pointer rounded md:text-2xl md:px-2 py-2 mx-8 md:my-8 font-semibold shadow bg-main 	text-white">
        {props.saludo}
        {props.link && <Link to={props.link} className="absolute right-10 hidden md:block mt-2 text-base cursor-pointer hover:text-black">{props.title}</Link>}
      </div>
    </Fragment>
  );
};
export default Card;
```

Cómo ejecución el resultado obtenido del código es lo que se visualiza en la imagen.

![](https://i.imgur.com/oKX0UsN.jpg)
 
 [Subir](#top)


<a name="item9"></a>
### CategorySectionCard
 ---
Componente utilizado para las imágenes de las categorías.

Este componente recibe los siguientes parámetros:  
img: Imagen de fondo.  
name: Nombre de la categoría.  
categoryId: Id de la categoría.  
withoutPaddingY: Son variables lógicas que se encarga del Padding del diseño de la cajita de categoría.  
withoutBgCover: Son variables lógicas que se encarga de escalar la imagen para que ocupe toda la caja. Solo son llamadas si deseo que se muestre o no.  

#### Código
```
import clsx from "clsx";
import { forwardRef } from "react";
const CategorySectionCard = forwardRef(({
    className,
    img,
    name,
    categoryId,
    withoutPaddingY = false,
    withoutBgCover = false,
}, ref) => {
    return (
        <a href={`/recipes?categoryId=${categoryId}`}>
            <div
                ref={ref}
                className={clsx(`
                flex items-center justify-center
                relative 
                w-full
                rounded-md
                transition transform hover:-translate-y-1
                hover:drop-shadow-2xl
                duration-300
                cursor-pointer
            `, {
                    'py-10': !withoutPaddingY,
                    'bg-cover': !withoutBgCover,
                }, className)}
                style={{ backgroundImage: `url(${img})`, backgroundSize: "100% 100%" }}
            >
                <div className='rounded-md absolute bg-black h-full w-full opacity-30' >
                </div>
                <div className="relative text-white text-center text-2xl" style={{ textShadow: "0px 0px 3px #000000" }} >
                    {name}
                </div>
            </div>
        </a>
    );
})export default CategorySectionCard;
```

Cómo ejecución del código se muestra su resultado en pantalla.

![](https://i.imgur.com/X0b6gXh.jpg)

[Subir](#top)

<a name="item10"></a>
### PopularSearch
 ---
Rectángulo con estilos específicos donde se agrega la información popular, imagen y texto de una sección publicitaria. 

Este componente recibe dos parámetros tipo string:  
img: Imagen de la sesión de popular.  
title: Título de la publicidad.  
url: url de la publicidad.

Importación de la libreria react-router-dom Consulte la guía de inicio para obtener más información sobre cómo comenzar con El paquete react-router-dom contiene enlaces para usar React Router en aplicaciones web. 

```
import React from 'react';
import { Link } from 'react-router-dom';

const PopularSearch = ({ title, img, url }) => {
    return (
        <div className="flex bg-white w-full rounded-md overflow-hidden shadow-md">
            <div className='justify-around items-center py-3 px-4 w-full'>
                <div className='text-3xl px-4 py-3 font-bold'>
                    {title}
                </div>
                <br />
                <Link to={url} className="bg-main text-white py-2 px-3 rounded my-4 mx-4">
                    See more
                </Link>
            </div>
            <div className="w-full">
                <img className='w-full h-full' src={img} alt="PopularSearch" />
            </div>
        </div>
    );
}
export default PopularSearch;
```
Cómo ejecución del código se muestra su resultado en pantalla.

![](https://i.imgur.com/epl8lQh.jpg)

[Subir](#top)

<a name="item11"></a>
### SwiperWeightPlan
 ---
Sección de los planes, donde se trae información de los planes como imagen, título y descripción breve.  

No recibe ningún parámetro.

Importación de la libreria useEffect, los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente.

Importación de la líbreria useState es un React Hook que le permite agregar una variable de estado a su componente.

#### Código

```
import React, { useState, useEffect } from "react";
import { Swiper, SwiperSlide } from "swiper/react";
import "swiper/css";
import "swiper/css/pagination";
import "swiper/css/navigation";
import WeightPlan from '../componentes/WeightPlan';
import { Navigation } from "swiper";
import usePlans from "../hooks/usePlans";
import SystemInfo from "../util/SystemInfo";

const SwiperWeightPlan = () => {
    const [innerWidth, setInnerWidth] = useState(window.innerWidth);

    const [filters, setFilters] = useState({
        page: 1,
        perPage: 10,
        hideClientPlans: 'true'
    })

    const [{ plans }] = usePlans({
        params: {
            ...filters
        }
    });

    useEffect(() => {
        const resizeHandler = () => {
            setInnerWidth(window.innerWidth);
        };

        window.addEventListener('resize', resizeHandler);

        return () => window.removeEventListener('resize', resizeHandler);
    }, []);

    return (
        <div className="container px-8">
            <Swiper
                slidesPerView={innerWidth > 768 ? 3 : 1}
                spaceBetween={20}
                loop={true}
                navigation={true}
                modules={[Navigation]}
                className="mySwiper m-auto "
            >
                {plans.map(plan => <SwiperSlide key={plan.id}>
                    <WeightPlan
                        price={`${plan?.price}$`}
                        hideCart
                        logo={`${SystemInfo.api}${plan?.seller?.logo}`}
                        img={`${SystemInfo.api}${plan?.images?.[0]?.path}`}
                        title={plan?.name}
                        text={plan?.description}
                    />
                </SwiperSlide>)}
            </Swiper>
        </div>
    );
}

export default SwiperWeightPlan;
```

Cómo ejecución de código se muestra lo que se vera en la imagen.
![](https://i.imgur.com/XTwqKMq.jpg)
 
 [Subir](#top)


<a name="item12"></a>
### CategoriesVideo
 ---
Toda la sección de categorías con videos. 

No recibe ningún parámetro.

#### Código

```
import category from "../assets/category3.jpg"
import CategorySectionCard from "./CategorySectionCard";
import React from 'react';
import SesionCategory from "./SesionCategory";
import VideoCategory from "./VideoCategory";

const CategoriesVideo = () => {
    return (
        <div className="bg-white">
            <div className="container p-4 ">
                <SesionCategory />
                <div className=" md:p-8 md:flex">
                    <div className="md:w-8/12 p-1">
                        <VideoCategory />
                    </div>
                    <div className="md:w-4/12 p-2 ">
                        <CategorySectionCard
                            img={category}
                            name="Paleo"
                            className={"py-40 bg-full"}
                            withoutPaddingY
                            withoutBgCover
                        />
                    </div>
                </div>
            </div>
        </div>

    );
}

export default CategoriesVideo;
```

Cómo ejecución se observa lo siguiente.

![](https://i.imgur.com/OcBFt3l.jpg)

[Subir](#top)
 
<a name="item13"></a>
* ### SesionCategory
 ---
Select de las categorías.  

No tiene ningún parámetro.

#### Código

```
const SesionCategory = () => {
    return (
        <form className="m-10 ml-8 m-50 cursor-pointer ">
            <select className="text-main font-semibold text-lg bg-white border border-gray-400 rounded-md py-1.5 md:px-20  
                         focus:border-gray-300 focus:ring focus:ring-gray-200 focus:ring-opacity-50 leading-4">
                <option value="">New recipes</option>
                <option value="">Low in calories</option>
                <option value="">Paleo</option>
                <option value="">High in protein </option>
            </select>
        </form >
    );
}
export default SesionCategory;
```
Cómo ejecución se observa lo siguiente.

![](https://i.imgur.com/lVviHpJ.jpg)

[Subir](#top)
 
<a name="item14"></a>
* ### VideoCategory
 ---
Descripción del vídeo, contiene imagen y nombre del vendedor, nombre de la receta.  

Cómo parámetro no recibe nada.

#### Código
```
import React from 'react';
import Video from './Video';

const VideoCategory = () => {
    return (
        <div className="h-full md:w-full grid md:grid-cols-3 md:gap-3">
            <Video name="Recipes Paleo" subname="Rosa Maria" />
            <Video name="Recipes Paleo" subname="Rosa Maria" />
            <Video name="Recipes Paleo" subname="Rosa Maria" />
            <Video name="Recipes Paleo" subname="Rosa Maria" />
            <Video name="Recipes Paleo" subname="Rosa Maria" />
            <Video name="Recipes Paleo" subname="Rosa Maria" />
        </div>
    );
}
export default VideoCategory;
```
Cómo ejecución se observa lo siguiente.

![](https://i.imgur.com/BlF8cca.jpg) 

[Subir](#top)


<a name="item15"></a>
* ### Video
 ---
Modelo de la estructura de la card donde se muestra el video.

Este componente recibe dos parámetros tipo string:  
name: recibe el nombre de vídeo.  
subname: Título de la publicidad.  

Importación de la líbreria react-player Componente react para reproducir una variadad de URL, incluidas rutas de archivos y YouTube.

#### Código
```
import ReactPlayer from 'react-player';
import chefsSw from '../assets/chefsSw.jpg';

const Video = ({ name, subname }) => {
    return (
        <div className="text-white">
            <div className="h-36 bg-black rounded-lg overflow-hidden">
                <ReactPlayer
                    url='https://www.youtube.com/watch?v=WmLNXXlo3rQ'
                    height={'100%'}
                    width={'100%'}
                    className="rounded-lg"
                />
            </div>
            <div className="flex">
                <img className="rounded-full h-10 w-10" src={chefsSw} alt="" />
                <div className="grid grid-rows-2 m-0.5">
                    <p className="text-black font-semibold ">{name}</p>
                    <p className="text-gray-500 text-xs font-semibold ">{subname}</p>
                </div>
            </div>
        </div>
    );
}
export default Video;
```

Cómo ejecución se observa lo siguiente.
![](https://i.imgur.com/GTLA87F.png)
 
[Subir](#top)


<a name="item16"></a>
### Recipes
 ---
Componente que contiene la estructura de la plantilla de como se muestra la receta en el home. 

Cómo parametro en el componente recibe { title, descsh, desccost, cost, img, level, time, ing, withDefaultButtons = true }

Importación de la líbreria react-icons que utiliza importaciones de ES6 que le permiten incluir solo los íconos que usa su proyecto.

#### Código
```
import { AiFillStar } from "react-icons/ai";
import { AiOutlineStar } from "react-icons/ai";
import { AiOutlineClose } from "react-icons/ai";
import { AiOutlineCheck } from "react-icons/ai";
import { BsFillEmojiLaughingFill } from "react-icons/bs";

const Recipes = ({ title, descsh, desccost, cost, img, level, time, ing, withDefaultButtons = true }) => {

    return (
        <div className="lg:flex bg-white rounded-md overflow-hidden shadow-md">
            <div className="lg:w-5/12">
                <img className='sm:h-32 md:h-56 lg:h-72 w-full md:block rounded-md' src={img} alt="Recipes" />
            </div>
            <div className="xl:flex py-4 px-4 md:h-full lg:w-7/12">
                <div className='mr-4 md:m-0 w-4/5'>
                    <div className='font-bold text-xl'>
                        {title?.length > 15 ? `${title.slice?.(0, 15)}...` : title}
                    </div>
                    <p className="px-1 mt-2 text-gray-400 text-xs">{descsh?.length > 25 ? `${descsh.slice?.(0, 25)}...` : descsh}</p>
                    <div className="flex">
                        <AiFillStar className="mt-2 text-yellow-300" />
                        <AiFillStar className="mt-2 text-yellow-300" />
                        <AiFillStar className="mt-2 text-yellow-300" />
                        <AiFillStar className="mt-2 text-yellow-300" />
                        <AiOutlineStar className="mt-2 text-gray-300" />
                    </div>
                    <div className="">
                        <div className="flex px-2 py-2 text-gray-400 text-xs">
                            <p className="w-1/2">Level</p>
                            <p className="w-1/2">{level}</p>
                        </div>
                        <div className="flex px-2 py-2 text-gray-400 text-xs">
                            <p className="w-1/2">Time</p>
                            <p className="w-1/2">{time}</p>
                        </div>
                        <div className="flex px-2 py-2 text-gray-400 text-xs">
                            <p className="w-1/2">Ingredients</p>
                            <p className="w-1/2 text-red-400">{ing}</p>
                        </div>
                    </div>
                </div>
                <div className="lg:w-2/5 justify-between lg:justify-start items-center flex lg:flex-col">
                    <div className='px-1 py-1 font-bold text-base'>
                        {cost}
                    </div>
                    <p className="px-1 py-1 text-gray-400 text-xs">{desccost}</p>

                    <div className="bottom-0 right-0 space-x-3 flex lg:justify-end items-center mt-auto">
                        {withDefaultButtons
                            ? <>
                                <button className="bg-white rounded-full py-1 px-1 shadow-2xl recipe-btn"><AiOutlineClose className="text-red-500" /></button>
                                <button className="bg-white rounded-full py-1 px-1 shadow-2xl recipe-btn" ><BsFillEmojiLaughingFill className="text-yellow-300" /></button>
                                <button className="bg-white rounded-full py-1 px-1 shadow-2xl recipe-btn" ><AiOutlineCheck className="text-green-700" /></button>
                            </>
                            : <>
                                <button className="bg-red-500 hover:bg-red-700 text-white font-bold md:py-2 md:px-4 py-1.5 px-2 text-base rounded"> Dismiss</button>
                                <button className="bg-main hover:bg-main-dark text-white font-bold md:py-2 md:px-4 py-1.5 px-2 text-base rounded"> Select</button>
                            </>
                        }
                    </div>
                </div>
            </div>
        </div>
    );
}export default Recipes;
```
Cómo ejecución se observa lo siguiente.

![](https://i.imgur.com/R1kSxvW.jpg) 
 
[Subir](#top)

<a name="item17"></a>
### ChefsCountries
 ---
Contiene sección de chefs populares por países. 

Este componente recibe los siguientes parámetro d etipo string:
imgChefs: Aquí recibe la imagen del chef.
LogoBackg: Imagen de fondo.
imgFlag: Imagen de la bandera.
name: Nombre del chef.
sname: Apellido del chef.

```
const ChefsCountries = ({ imgChefs, LogoBackg, imgFlag, name, sname }) => {
    return (
        <div className="mdflex relative h-80 md:w-96 rounded-md cursor-pointer mt-10 mr-5 ml-5 mb-10 bg-cover" style={{ backgroundImage: `url(${LogoBackg})` }}>
            <div className="absolute bg-black opacity-30 rounded-md w-full h-full">
            </div>
            <div className='absolute bg-white left-1/2 top-[30px] h-20  transform -translate-x-1/2 rounded shadow-md'>
                <img className="rounded-lg top-[40px] h-20 w-20 " src={imgChefs} alt="Chefs" />
            </div>
            <div className='absolute bg-white left-1/2 top-[140px] h-20  transform -translate-x-1/2 rounded shadow-md'>
                <img className="h-20 w-40 " src={imgFlag} alt="Flag" />
            </div>
            <div className="absolute font-sans text-white bottom-0 right-0 py-4 px-4 text-2xl">
                <div className="text-center font-sans text-white bottom-0 right-0 text-2xl" style={{ textShadow: "0px 0px 3px #000000" }}>
                    {name}
                </div>
                <div className="font-sans text-white bottom-0 right-0 text-2xl" style={{ textShadow: "0px 0px 3px #000000" }}>
                    {sname}
                </div>
            </div>

        </div>
    );
}

export default ChefsCountries;
```
Cómo ejecución se observa lo siguiente.

![](https://i.imgur.com/s8M3PYt.jpg) 
 
[Subir](#top)

<a name="item18"></a>
### AuthModal
 ---
Este componente es el encargado de la validación de escuchar el clic al seleccionar el Button de inicio de sesión donde nos permite iniciar en la vista del login o en la vista del registro.

Recibe como parámetro { show, onClose } show, lo que hace es avisar al componente padre en que modal estoy y onClose me permite cerrar el modal donde se encuentre.

Importación de la libreria useEffect, los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente.

Importación de la líbreria useState es un React Hook que le permite agregar una variable de estado a su componente.

#### Código
```
import { useRef, useState } from "react";
import ReactDom from "react-dom";
import ForgotPasswordForm from "./ForgotPasswordForm";
import LoginForm from "./LoginForm";
import RegisterForm from "./RegisterForm";

const AuthModal = ({ show, onClose }) => {

    const [showForm, setShowForm] = useState('login');

    const modalRef = useRef();

    if (!show) {
        return null;
    }

    const handleClose = (e, forceClose) => {
        if (forceClose) {
            onClose();
            return;
        }


        if (modalRef.current === e.target) {
            onClose();
        }
    }

    const handleForm = (form) => {
        setShowForm(form);
    }

    return ReactDom.createPortal(
        <div ref={modalRef} onClick={handleClose} className="flex h-screen w-screen bg-black bg-opacity-50 fixed z-10 p-10" style={{ top: 0, left: 0, overflowY: 'auto' }}>
            {
                showForm === 'login' &&
                <LoginForm changeForm={handleForm} onClose={onClose} />
            }

            {
                showForm === 'forgot-password' &&
                <ForgotPasswordForm changeForm={handleForm} onClose={onClose} />
            }

            {
                showForm === 'register' &&
                <RegisterForm changeForm={handleForm} onClose={onClose} />
            }
        </div>
        ,
        document.getElementById("portal")
    );
}export default AuthModal;
```
Cómo ejecución se observa lo siguiente.

![](https://i.imgur.com/sv9LjAY.jpg)  
 
[Subir](#top)


<a name="item19"></a>
### ButtonSupr
 ---
Componente con las dos opciones de vista (Grid View, ListView). en las pantallas de resultados de busqueda.

Cómo parámetro no recibe ninguno.
```
import { IoList, IoGridOutline } from "react-icons/io5";

const ButtonSupr = () => {
    return (
        <div className="flex justify-end space-x-6">
            <button className="flex items-center space-x-2 text-main hover:text-main-dark">
                <IoGridOutline />
                <span>Grid View</span>
            </button>
            <button className="flex items-center space-x-2 hover:text-main">
                <IoList />
                List View
            </button>
            <span className="hover:text-main">
                <b>117</b>
                Recipes
            </span>
        </div>
    );
}export default ButtonSupr;
```
Cómo ejecución se observa lo siguiente.

![](https://i.imgur.com/oblMl0x.jpg)

[Subir](#top)



<a name="item20"></a>
### MenuLeft
 ---
Este componente es el encargado de la estructura del sistema de filtrado que aparece en el lateral izquierdo en las pantallas de resultados de búsqueda.  A su vez contiene 6 componentes.   

Este componente recibe como parámetro { filters, onClickCategory, onChangeRating, className, style } son variables para el funcionamiento del menú lateral.
filters: Variable tipo string de flitro de selección.
onClickCategory: Variable de valor lógico de la escucha el click de categoría.
onChangeRating: Variable de valor lógico de la escucha el click del rating.
className: Esté parametro recibe una clases de que tu le quieras pasar.
style: Aquí en esta variable recibe el estilo.

#### Código
```
import ButtonRank from "./ButtonRank";
import CategoriesRecipes from "./CategoriesRecipes";
import RatingComponent from "./RatingComponent";
import SelectCategory from "./SelectCategory";
import SelectRank from "./SelectRank";

const MenuLeft = ({ filters, onClickCategory, onChangeRating, className, style }) => {
    return (
        <div
            style={style}
            className={`hidden md:block ${className || ''}`}
        >

            <div className="lg:ml-6 bg-white lg:w-64 w-56 m-auto md:w-40 rounded-lg shadow ">
                <CategoriesRecipes onClickCategory={onClickCategory} values={filters?.categoryIds} />
            </div>
            <div>
                <div className="p-4 mt-6 lg:ml-6 bg-white lg:w-64 m-auto w-56 md:w-40 rounded-lg shadow">
                    <p className="title-medium mt-2 mb-6">Types</p>
                    <SelectCategory title="Breakfast" />
                    <SelectCategory title="Lunch" />
                    <SelectCategory title="Dinner" />
                    <SelectCategory title="Snacks" />
                </div>
            </div>
            <div>
                <div className="p-4 mt-6 lg:ml-6 bg-white lg:w-64 w-56 m-auto md:w-40 rounded-lg shadow">
                    <h1 className="title-medium mt-2 mb-6">Rating</h1>
                    <div className="flex items-center space-between">
                        <RatingComponent
                            onClickStar={onChangeRating}
                            value={filters?.rating}
                        />
                        {
                            filters?.rating &&
                            <button className="bg-main rounded-xl text-white px-4 py-1" onClick={() => onChangeRating('')}>
                                Clear
                            </button>
                        }
                    </div>
                </div>
            </div>
        </div>
    );
}export default MenuLeft;
```
Cómo ejecución se observa lo siguiente.

![](https://i.imgur.com/25UWgjQ.png) 
 
[Subir](#top)



<a name="item21"></a>
### CategoriesRecipes
 ---
Componente encargado del filtrado por categorías del menu lateral, donde se puede observar las categorias cargadas en la base de datos.

Recibe como parámetro { onClickCategory, values } onClickCategory, nos permite almacenar un valor en especifico para saber si seleccione click a la categoria y value es un arreglo de id de categorias que es llenada por el componente superior que lo llama.

Importación de la librería useCallback useCallback en React tiene un uso muy similar al hook useMemo, pues ambos se enfocan en memoizar ciertos elementos en React. La diferencia aquí es que, mientras useMemo devuelve un valor memoizado, el hook useCallback devuelve una función memoizada.

Importación de la librería useRef en React nos devuelve un objeto ref mutable, cuya propiedad current se inicializa en el argumento pasado como initialValue:
const refContainer = useRef (initialValue)

Importación de la libreria useEffect, los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente.

Importación de la líbreria useState es un React Hook que le permite agregar una variable de estado a su componente.

#### Código
```
import clsx from "clsx";
import React, { useCallback, useEffect, useRef, useState } from "react";
import useCategories from "../hooks/useCategories";

const CategoriesRecipes = ({ onClickCategory, values }) => {

  const [categoriesFilters, setCategoriesFilters] = useState({
    page: 1,
    perPage: 8
  });

  const [currentCategories, setCurrentCategories] = useState([]);

  const [{ categories, numberOfPages, error, loading }, getCategories] = useCategories({ axiosConfig: { params: { ...categoriesFilters } }, options: { useCache: false } });

  const observer = useRef();

  const lastValueRef = useCallback((value) => {
    if (observer?.current) observer?.current?.disconnect?.();

    observer.current = new IntersectionObserver(entries => {
      if (entries[0].isIntersecting) {
        if (numberOfPages > categoriesFilters?.page) {
          setCategoriesFilters((oldCategories) => {
            return {
              ...oldCategories,
              page: oldCategories?.page + 1
            }
          });
        }
      }
    })
    if (value) observer?.current?.observe?.(value)
  }, [currentCategories]);

  useEffect(() => {
    if (categories?.length > 0) {
      setCurrentCategories((oldCategories) => {
        return [...oldCategories, ...categories]
      });
    }
  }, [categories]);

  return (
    <div className="mb-4 md:p-6">
      <h4 className="title-medium mt-2 mb-6">Categories</h4>
      {
        values?.length > 0 &&
        <div className="text-end">
          <button className="bg-main rounded-xl text-white px-4 py-1" onClick={() => onClickCategory('')}>
            Clear
          </button>
        </div>
      }
      <div style={{ maxHeight: '300px', overflowY: 'auto' }} className="custom-scrollbar custom-scrollbar-main">
        {
          currentCategories?.map((category, i) => {
            return (
              <div
                key={i}
                onClick={() => { onClickCategory?.(category) }}
                ref={i + 1 === currentCategories.length ? lastValueRef : null}
                className={clsx(["font-normal cursor-pointer hover:text-main m-2"], {
                  "text-main": values?.includes(category?.id)
                })}
              >
                {category?.name}
              </div>
            )
          })
        }
        {
          loading &&
          <div
            className="font-normal cursor-pointer hover:text-main m-2"
          >
            Loading...
          </div>
        }
      </div>
    </div>
  );
};

export default CategoriesRecipes;
```
Cómo resultado de la ejecución se puede visualizar en la imagen.

![](https://i.imgur.com/nodHnhR.jpg) 
 
[Subir](#top)



<a name="item22"></a>
### SelectCategory
 ---
Componente encargado del filtrado por Types.

Cómo parámetro no recibe nada.

#### Código
```
const SesionCategory = () => {
    return (
        <form className="m-10 ml-8 m-50 cursor-pointer ">
            <select className="text-main font-semibold text-lg bg-white border border-gray-400 rounded-md py-1.5 md:px-20  
                         focus:border-gray-300 focus:ring focus:ring-gray-200 focus:ring-opacity-50 leading-4">
                <option value="">New recipes</option>
                <option value="">Low in calories</option>
                <option value="">Paleo</option>
                <option value="">High in protein </option>
            </select>
        </form >
    );
}

export default SesionCategory;
```
Cómo resultado de la ejecución se puede visualizar en la imagen.

![](https://i.imgur.com/7mNZHhE.png)
 
[Subir](#top)



<a name="item23"></a>
### SelectRank
 
Componente encargado del filtrado por Ranking. 
Cómo parámetro recibe el { num }  donde su valor es un número entero. encargado de el promedio del recorrido de array con el número recibido por parámetro.

Importación de la líbreria react-icons que utiliza importaciones de ES6 que le permiten incluir solo los íconos que usa su proyecto.

#### Código
```
import React from "react";
import { FaRegStar } from "react-icons/fa";
import Checkbox from "./Checkbox";

const SelectRank = ({ num }) => {
  return (
    <div className="flex ">
      <div className="justify-end form-check md:px-1 px-2">
        <Checkbox className="mb-4 mt-1.5" />
      </div>
      <div className="flex text-yellow-300 lg:ml-2 md:ml-0 md:text-lg text-xl md:space-x-1 space-x-2">
        {Array.from(Array(num - 1).keys()).map(n => <FaRegStar
          key={n}
          className="lg:w-6 lg:h-6  text-yellow-400"
        />)}
      </div>

    </div >
  );
};

export default SelectRank;
```
Cómo resultado de la ejecución se puede visualizar en la imagen.

![](https://i.imgur.com/jXqV6aG.png)
 
[Subir](#top)



<a name="item24"></a>
### ButtonRank 
 
Componente con botones para aplicar o resetear los filtros.
Cómo parámetro no recibe ninguno.

#### Código
```
const ButtonRank = () => {
    return (
        <div className="lg:flex lg:space-x-8">
            <button className="bg-main mt-14 mb-4 ml-2 text-white hover:bg-main-light hover:text-white font-bold py-2 px-4 rounded-lg">
                Apply
            </button>
            <button className="bg-main mt-14 mb-4 ml-2 text-white hover:bg-main-light hover:text-white font-bold py-2 px-4 rounded-lg">
                Reset
            </button>
        </div>
    );
}

export default ButtonRank;
```
Cómo resultado de la ejecución se puede visualizar en la imagen.

![](https://i.imgur.com/liIgGmE.png)

[Subir](#top)



<a name="item25"></a>
### BannerChef
 
Este componente contiene la estructura de las cards con la información mostrada de cada vendedor desde la vitrina de vendedores y el home.

Cómo parámetro recibe el id del seller "valor de tipo entero".

Importación de la libreria useEffect, los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente.

Importación de la líbreria useState es un React Hook que le permite agregar una variable de estado a su componente.

Importación de la libreria react-router-dom Consulte la guía de inicio para obtener más información sobre cómo comenzar con El paquete react-router-dom contiene enlaces para usar React Router en aplicaciones web.

#### Código

```
import { BsStarFill } from "react-icons/bs";
import cheque from "../assets/cheque.png";
import { Link } from "react-router-dom";
import imgUrl from "../helpers/imgUrl";
import RatingComponent from "./RatingComponent";
import Modal from "./Modal/Modal";
import { useState } from "react";
import useSellersRatings from "../hooks/useSellersRatings";
import { useEffect } from "react";


const BannerChef = ({ seller }) => {

  const [showCustomersReviews, setShowCustomersReviews] = useState(false);

  const [currentReviews, setCurrentReviews] = useState([]);

  const [filters, setFilters] = useState({
    page: 1,
    orderBy: 'createdAt,DESC',
    sellerId: ''
  });

  const [{ sellersRatings, numberOfPages: ratingPages, total: totalReviews, loading: loadingRatings }, getRatings] = useSellersRatings({ params: { ...filters }, options: { manual: true, useCache: false } });

  useEffect(() => {
    if (filters?.sellerId) {
      getRatings({
        params: {
          ...filters
        }
      });
    }
  }, [filters])

  useEffect(() => {
    if (sellersRatings?.length > 0) {
      setCurrentReviews((oldReviews) => {
        return [...oldReviews, ...sellersRatings];
      });
    }
  }, [sellersRatings]);

  useEffect(() => {
    if (seller?.sellerId) {
      setFilters((oldFilters) => {
        return {
          ...oldFilters,
          sellerId: seller?.sellerId
        }
      })
    }
  }, [seller?.sellerId])

  const handleMore = () => {
    if (ratingPages > filters?.page) {
      setFilters((oldFilters) => {
        return {
          ...oldFilters,
          page: oldFilters?.page + 1
        }
      });
    }
  }

  return (
    <div
      className="md:h-96 flex justify-center items-center"
      style={{ backgroundImage: `url(${imgUrl(seller?.banner)})`, backgroundSize: "100% 100%" }}
    >
      <div className="h-full w-full" style={{ background: "rgba(0,0,0, .5)" }}>
        <Link to={`/sellers/${seller?.slug}/blog`}>
          <div className="flex justify-center items-center p-6">
            <img src={imgUrl(seller?.logo)}
              className="md:h-52 md:w-52 w-20 h-20 rounded-full items-center" alt="" />
          </div>
        </Link>
        <div className="text-center text-white font-sans">
          <div className="flex justify-center text-center">
            <p className="md:text-4xl text-center font-bold text-ellipsis">{(seller?.name)}</p>
            <img src={cheque} alt="" className="md:mt-4 md:ml-3 m-1 text-main w-5 h-5" />
          </div>

          <p className="md:text-2xl">{(seller?.shortDescription)}</p>
          <div onClick={() => setShowCustomersReviews(true)} className="flex items-center justify-center cursor-pointer">
            <RatingComponent
              disabled
              value={seller?.rating}
            />
            ({totalReviews} customers reviews)
          </div>
        </div>
      </div>
      <Modal show={showCustomersReviews} onClose={() => setShowCustomersReviews(false)}>
        <div style={{ maxHeight: '70vh', overflowY: 'auto' }} className="custom-scrollbar custom-scrollbar-main">
          <h1 className="text-center text-xl font-bold">
            Customers Reviews ({totalReviews})
          </h1>
          {
            currentReviews?.length > 0 ?
              currentReviews?.map((review, i) => {
                return (
                  <div key={i} className="py-4 border-b border-main">
                    <div className="flex items-center space-x-4">
                      <img src={imgUrl(review?.client?.imgPath)} style={{ height: 50, width: 50 }} className="rounded-full" />
                      <p className="text-gray-500 font-bold">
                        {review?.client?.name}
                        <RatingComponent
                          disabled
                          value={review?.value}
                          size="sm"
                        />
                      </p>
                    </div>
                    <br />
                    <p className="text-gray-500">
                      {review?.comment}
                    </p>
                  </div>
                )
              })
              :
              <div className="text-center text-red-500 text-xl">
                No results found.
              </div>
          }
          {
            loadingRatings ?
              <div className="text-center my-4">
                Loading more reviews...
              </div>
              :
              ratingPages > filters?.page ?
                <div className="text-center">
                  <button onClick={handleMore} className="bg-white px-8 py-2 rounded-full shadow mt-4 mb-4">
                    Load More
                  </button>
                </div>
                :
                <div className="text-center my-4">
                  No more reviews.
                </div>
          }
        </div>
      </Modal>
    </div>
  );
};

export default BannerChef;
```
Cómo resultado de la ejecución se puede visualizar en la imagen.

![](https://i.imgur.com/KQQe1Zd.jpg)
 
[Subir](#top)



<a name="item26"></a>
### ButtomButton
 
Componente que contiene la llamada de un subcomponente llamado scroll de navegación.

No posee nigún parámetro.

#### Código
```
import ScrollNavigation from "../componentes/ScrollNavigation";

const ButtomButton = () => {
  return (
    <div>
      <ScrollNavigation />
    </div>
  );
};

export default ButtomButton;
```
Cómo ejecución del código, es la llamada al componente donde contiene el diseño del pies de pagina. A continuación se explica detalladamente el componente scrollNavigation.

### ScrollNavigation
 
Componente con botones de paginación que se repite en varias secciones.
Cómo parámetro no recibe ningun tipo de datos.

#### Código
```
import React from "react";
import { AiOutlineLeft, AiOutlineRight } from "react-icons/ai";
const ButtomButton = () => {
  return (
    <div className="flex flex-col items-center my-12">
      <div className="flex text-gray-700">
        <div className="h-12 w-12 mr-1 flex justify-center items-center rounded-full cursor-pointer  hover:bg-main hover:text-white">
          <AiOutlineLeft />
        </div>
        <div className="flex h-12 font-medium rounded-full space-x-2">
          <div className="w-12 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full  border border-main hover:bg-main hover:text-white">
            1
          </div>
          <div className="w-12 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full border border-main  hover:bg-main hover:text-white ">
            2
          </div>
          <div className="w-12 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full border border-main  hover:bg-main hover:text-white  ">
            3
          </div>
          <div className="w-12 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full ">
            ...
          </div>
          <div className="w-12 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full border border-main  hover:bg-main hover:text-white ">
            8
          </div>
          <div className="w-12 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full border border-main  hover:bg-main hover:text-white ">
            9
          </div>
          <div className="w-12 md:flex justify-center items-center hidden  cursor-pointer leading-5 transition duration-150 ease-in  rounded-full border border-main  hover:bg-main hover:text-white ">
            10
          </div>
          <div className="w-12 h-12 md:hidden flex justify-center items-center cursor-pointer leading-5 transition duration-150 ease-in rounded-full bg-main text-white ">
            1
          </div>
        </div>
        <div className="h-12 w-12 ml-1 flex justify-center items-center rounded-full cursor-pointer hover:bg-main hover:text-white">
          <AiOutlineRight />
        </div>
      </div>
    </div>
  );
};

export default ButtomButton;
```
![](https://i.imgur.com/7UNmpRB.jpg)
 
[Subir](#top)

<a name="item27"></a>
### ProductImagenCarousel

Componentes con la vista de las imagenes en el detalle del producto
Este componente recibe como parámetro.

Importación de la líbreria useState es un React Hook que le permite agregar una variable de estado a su componente.

Importación de la líbreria swiper de Por defecto, Swiper React usa la versión principal de Swiper (sin ningún módulo adicional). Si desea utilizar Navegación, Paginación y otros módulos , primero debe instalarlos.

#### Código
```
import clsx from "clsx";
import { useState } from "react";
import { Swiper, SwiperSlide } from 'swiper/react';
import imgUrl from "../helpers/imgUrl";

const ProductImagesCarousel = ({ images = [], productName }) => {
  const [swiper, setSwiper] = useState(null);

  const [activeSlideIndex, setActiveSlideIndex] = useState(0);

  return <div className="hidden md:block">
    <div className="relative">
      <Swiper
        onSwiper={setSwiper}
        onSlideChange={(swiper) => setActiveSlideIndex(swiper.activeIndex)}
        autoHeight={true}
      >
        {
          images?.length > 0 && images?.map(image => <SwiperSlide key={image.id} zoom={{ maxRatio: 2 }}>
            <div className="swiper-zoom-container">
              <img
                src={imgUrl(image.path)}
                alt={productName}
                className="rounded-xl w-full h-96"
              />
            </div>
          </SwiperSlide>)}
      </Swiper>
    </div>
    <div className="flex justify-center mt-6 space-x-3">
      {images?.length > 0 &&
        images?.map((image, i) => <img
          key={image.id}
          src={imgUrl(image.path)}
          alt={productName}
          className={clsx(
            'h-20 w-20 rounded-xl border border-gray-100 rounded shadow hover:shadow-md cursor-pointer',
            activeSlideIndex === i && 'ring-2 ring-blue-300 ring-opacity-75'
          )}
          onClick={() => swiper.slideTo(i)}
        />)}
    </div>
  </div>;
};

export default ProductImagesCarousel;
```
Cómo resultado de la ejecución del componente es el resultado final que se puede observar en la imagen.
![](https://i.imgur.com/6KCthjp.jpg)
 
[Subir](#top)




<a name="item28"></a>
### Matches
 
Botones de interaccion con funcionalidades para hacer match, agregar a favoritos o descartar un producto.

cómo parámetro no recibe ninguno este componente.

Importación de la líbreria react-icons que utiliza importaciones de ES6 que le permiten incluir solo los íconos que usa su proyecto.

#### Código
```
import React from 'react'
import {AiOutlineClose, AiOutlineCheck} from 'react-icons/ai'
import {BsFillEmojiLaughingFill} from "react-icons/bs"


const Matches = () => {
  return (
    <div className="container flex justify-center space-x-8">
        <button className="bg-white rounded-full py-2 px-2 shadow-2xl text-xl recipe-btn"><AiOutlineClose className="text-red-500" /></button>
        <button className="bg-white rounded-full py-2 px-2 shadow-2xl text-xl recipe-btn"><BsFillEmojiLaughingFill className="text-yellow-300" /></button>
        <button className="bg-white rounded-full py-2 px-2 shadow-2xl text-xl recipe-btn"><AiOutlineCheck className="text-green-700	" /></button>

    </div>
  )
}

export default Matches
```
Cómo resultado de la ejecución del componente es el resultado final que se puede observar en la imagen.

![](https://i.imgur.com/VrVdiMo.jpg)

[Subir](#top)



<a name="item29"></a>
### MenuConfig
 
Componente padre del menú desplegable del panel de usuario con iconos e item.

Recibe como parámetro { show, onClose } show, lo que hace es avisar al componente padre en que modal estoy y onClose me permite cerrar el modal donde se encuentre.

Importación de la libreria useEffect, los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente.

Importación de la líbreria useState es un React Hook que le permite agregar una variable de estado a su componente.

Importación de la líbreria react-icons que utiliza importaciones de ES6 que le permiten incluir solo los íconos que usa su proyecto.

Importación de la libreria react-router-dom Consulte la guía de inicio para obtener más información sobre cómo comenzar con El paquete react-router-dom contiene enlaces para usar React Router en aplicaciones web.

#### Código
```
import { useRef, useEffect } from "react";
import { FaUserCircle } from "react-icons/fa";
import { BsFillBookmarkHeartFill, BsFillGearFill, BsFillCalendar2MinusFill } from "react-icons/bs";
import { RiMessage2Fill } from "react-icons/ri";
import { AiOutlineLogout } from "react-icons/ai";
import { FaListAlt } from "react-icons/fa";
import { useAuth } from "../contexts/AuthContext";
import { IoHeart, IoHelpCircleOutline, IoChatbubbleEllipsesOutline, IoBookmarksSharp } from "react-icons/io5";
import { Link } from "react-router-dom";
import MenuList from "../util/MenuList";

const MenuConfig = ({ show, onClose }) => {
    const { setAuthInfo } = useAuth();

    const modalRef = useRef();

    const handleLougoutClick = (e) => {
        e.preventDefault();

        setAuthInfo({ isAuthenticated: false, token: null });
    }

    useEffect(() => {
        const handleMousedown = (e) => {
            if (modalRef.current && !modalRef.current.contains(e.target)) {
                onClose?.();
            }
        }

        document.addEventListener('mousedown', handleMousedown);

        return () => document.addEventListener('mousedown', handleMousedown);
    }, [modalRef])

    if (!show) {
        return null;
    }

    return (
        <div>
            <ul ref={modalRef}
                style={{ top: '100%' }}
                className="absolute space-y-2 z-20 right-0 text-white bg-gray-800 w-52 border border-slate-300 rounded-md py-4"
            >
                {
                    MenuList?.map(({ name, Icon, url }, i) => {
                        return (
                            <li className="space-x-2 border-b px-4" key={i}>
                                <Link to={url}>
                                    <div className="flex hover:text-main">
                                        <Icon className="mt-1" />
                                        <p className="text-lg ml-2.5 mb-1.5">{name}</p>
                                    </div>
                                </Link>
                            </li>
                        )
                    })
                }
                <li className="space-x-2 px-4">
                    <a onClick={handleLougoutClick} href="dfdf">
                        <div className="flex hover:text-main">
                            <AiOutlineLogout className="mt-1" />
                            <p className="text-lg ml-2.5">Log Out</p>
                        </div>
                    </a>
                </li>

            </ul>
        </div>
    );
}

export default MenuConfig;
```
Cómo resultado de la ejecución del componente es el resultado final que se puede observar en la imagen.

![](https://i.imgur.com/eKEAr1k.png)

[Subir](#top)




<a name="item30"></a>
### MyAccountLayout
 
Panel de herramientas del usuario vista con iconos.

El comnponente no recibe ningún parámetro.

Importación de la líbreria react-icons que utiliza importaciones de ES6 que le permiten incluir solo los íconos que usa su proyecto.

Importación de la libreria react-router-dom Consulte la guía de inicio para obtener más información sobre cómo comenzar con El paquete react-router-dom contiene enlaces para usar React Router en aplicaciones web.

Importación de la libreria useEffect, los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente.

Importación de la líbreria useState es un React Hook que le permite agregar una variable de estado a su componente.

#### Código
```
import clsx from "clsx";
import { useEffect, useState } from "react";
import { BsFillHeartFill, BsFillGearFill, BsFillBookmarkHeartFill, BsFillCalendar2MinusFill } from "react-icons/bs";
import { IoPersonCircleSharp } from "react-icons/io5";
import { FaListAlt } from "react-icons/fa";
import { RiMessage2Fill } from "react-icons/ri";
import { AiOutlineLogout } from "react-icons/ai";
import { Link, Outlet, useLocation } from "react-router-dom";
import { useAuth } from "../contexts/AuthContext";
import { IoHelpCircleOutline, IoChatbubbleEllipsesOutline, IoBookmarksSharp } from "react-icons/io5";
import MenuList from "../util/MenuList";

const MyAccountLayout = () => {
    const { setAuthInfo } = useAuth();

    const [currentPath, setCurrentPath] = useState("");

    const location = useLocation();

    useEffect(() => {
        setCurrentPath(location?.pathname);
    }, [location]);

    const handleLougoutClick = (e) => {
        e.preventDefault();

        setAuthInfo({ isAuthenticated: false, user: null, token: null });
    }

    return (
        <div className="flex">
            <div className="w-2/12 md:w-[5vw] bg-gray-700 hidden md:block text-white text-[2vw]" >
                {
                    MenuList?.map(({ name, Icon, url }, i) => {
                        return (
                            <div key={i}>
                                <Link title={name} to={url}>
                                    <Icon className={clsx(["mx-auto my-6 cursor-pointer transform hover:text-main hover:scale-150 transition duration-500 text-3xl md:text-2xl"], {
                                        'text-main': currentPath === url
                                    })} />
                                </Link>
                            </div>
                        )
                    })
                }
                <div className="text-center">
                    <button title="Log Out" onClick={handleLougoutClick} className="mx-auto my-6 cursor-pointer transform hover:text-main hover:scale-150 transition duration-500 text-3xl md:text-2xl">
                        <AiOutlineLogout ></AiOutlineLogout>
                    </button>
                </div>
            </div>
            <div className="w-full min-w-0">
                <Outlet />
            </div>
        </div >
    );
}

export default MyAccountLayout;
```
Cómo ejecución del código su resultado final es lo que se puede visualizar en la imagén.

![](https://i.imgur.com/ftYgUpz.png)
 
[Subir](#top)




<a name="item31"></a>
### PageLogo
 
Componente con el logo de la app que se adapta al tamaño adecuado.

Cómo parámetro recibe { centered = false } es una variable logica que tepermite mostrar o no el lolo del sistema.

Importación de la libreria react-router-dom Consulte la guía de inicio para obtener más información sobre cómo comenzar con El paquete react-router-dom contiene enlaces para usar React Router en aplicaciones web.

#### Código
```
import { Link } from 'react-router-dom';
import LogoDrafts from '../assets/drafts.png';

const PageLogo = ({ centered = false }) => {
    return (
        <Link to={"/"}>
            <div className={`flex items-center text-white md:space-x-4 ${centered ? 'justify-center' : ''}`}>
                <img className="inline-block md:h-9 w-9 rounded-lg"
                    src={LogoDrafts} alt="recipes" />
            </div>
        </Link>
    );
}

export default PageLogo;
```
Cómo ejecución del código su resultado final es lo que se puede visualizar en la imagén.

![](https://i.imgur.com/2sY7Kq7.jpg)
 
[Subir](#top)



<a name="item33"></a>
### CertificationChef
 
Componente con informacion profesional del vendedor desde su perfil.

Cómo parámetro recibe el seller que seria de tipo entero el identificador del seller.

Importación de la líbreria react-icons que utiliza importaciones de ES6 que le permiten incluir solo los íconos que usa su proyecto.

#### Código

```
import React from "react";
import { BsPatchCheckFill } from "react-icons/bs";

const CertificationChef = ({ seller }) => {
  return (
    <div className="mt-6 p-2">
      <button className="flex items-center space-x-2 text-black text-lg	 font-semibold">
        <BsPatchCheckFill className="text-main" />
        <span>Professional Certification</span>
      </button>
      <div className=" mt-4">
        <h1>Chef: {seller?.credentialNumber}</h1>
      </div>
    </div>
  );
};
export default CertificationChef;
```
Cómo ejecución del código su resultado final es lo que se puede visualizar en la imagén.

![](https://i.imgur.com/0FU20yz.jpg)
 
[Subir](#top)


<a name="item34"></a>
### Post
 
Entradas del blog del vendedor ubicadas en el lateral izquierdo del perfil del vendedor.

No recibe ningún parámetro.

Importación de la líbreria react-icons que utiliza importaciones de ES6 que le permiten incluir solo los íconos que usa su proyecto.

#### Código
```
import { BsPin } from "react-icons/bs";
import React from "react";

const Post = () => {
  return (
    <div className="mt-12">
      <h1 className="text-xl font-semibold">Post De Anya</h1>
      <div className="mt-6">
        <div className=" space-y-3">
          <button className="flex items-center space-x-2 text-black ">
            <BsPin className="text-main" />
            <span>5 Formas para Picar Cebolla.</span>
          </button>
          <button className="flex items-center space-x-2 text-black">
            <BsPin className="text-main" />
            <span>Tips para mejorar tus jugos.</span>
          </button>
          <button className="flex items-center space-x-2 text-black">
            <BsPin className="text-main" />
            <span>5 Formas para Picar Cebolla.</span>
          </button>
          <button className="flex items-center space-x-2 text-black">
            <BsPin className="text-main" />
            <span>Mantén afilados tus cuchillos.</span>
          </button>
          <button className="flex items-center space-x-2 text-black">
            <BsPin className="text-main" />
            <span>Utiliza papel de hornear.</span>
          </button>
          <button className="flex items-center space-x-2 text-black">
            <BsPin className="text-main" />
            <span>Siempre utiliza aceite de oliva.</span>
          </button>
        </div>
      </div>
    </div>
  );
};

export default Post;
```
Cómo ejecución del código su resultado final es lo que se puede visualizar en la imagén.

![](https://i.imgur.com/k4IAEZ8.jpg)
 
[Subir](#top)



<a name="item35"></a>
### DescriptionChef
 
Descripcion escrita por el vendedor en su perfil.

Cómo parámetro recibe el seller que seria de tipo entero el identificador del seller.

Importación de la líbreria react-icons que utiliza importaciones de ES6 que le permiten incluir solo los íconos que usa su proyecto.

#### Código
```
import React from "react";
import { RiBookReadLine } from "react-icons/ri";

const DescriptionChef = ({ seller }) => {
  return (
    <div className="mt-10 p-2">
      <button className="flex items-center space-x-2 text-black text-xl font-semibold">
        <RiBookReadLine className="text-main" />
        <span>Description</span>
      </button>
      <div className="p-1 md:text-justify text-justify ">
        {seller?.description}
      </div>
    </div>
  );
};

export default DescriptionChef;
```
Cómo ejecución del código su resultado final es lo que se puede visualizar en la imagén.

![](https://i.imgur.com/lOrkBhB.jpg)
 
[Subir](#top)


<a name="item36"></a>
### ButtonImage
 
Este componente contiene los botones de opcion de compra de ingredientes en Wallmart, Insta card y Amazon Fresh, los cuales redireccionan hacia estos sitios para realizar la compra con esos supermercados. Asi mismo se encuentra dentro de este el boton de pago del producto (receta, plan o combo) a traves de pay pal. 

Recibe como parámetro { image } una imagen que es la que va en el button.

#### Código
```
const ButtonImage = ({ image }) => {
    return (
        <button
            style={{ backgroundImage: `url(${image})`, backgroundSize: '100% 100%', backgroundPosition: 'center center' }}
            className="mb-4 p-2 mb:ml-2 w-40 h-12 rounded-xl border bg-white">
        </button>
    )
}
export default ButtonImage;
```
Cómo ejecución del código del resultado final es lo que se muestra en la imagen.
![](https://i.imgur.com/kXCgkaW.jpg) 
![](https://i.imgur.com/ZSwrYTC.jpg)
 
[Subir](#top)


<a name="item37"></a>
### Details
 
Componentes encargado de mostrar esta información que se encuentra en la vista de detalle de recetas, combos y planes (Level, categoria, time, igredientes).

Recibe parámetro { level, categories, fitness, time, days, ingredients, number, price, hideprice = false }, la variable hideprice es una variable logica porque permite ocultar una linea en epecifico, las demas variables son de tipo string.

#### Código
```
import React from 'react'
import Chefs from '../assets/chef-hat.png'
const Details = ({ level, categories, fitness, time, days, ingredients, number, price, hideprice = false }) => {
    return (
        <div>
            <div className='md:flex py-2 '>
                <p className="w-1/2">{level}</p>
                <div className='flex mt-1'>
                    <img className="w-6 h-6" src={Chefs} alt="chefs" />
                    <img className="ml-2 w-6 h-6" src={Chefs} alt="chefs" />
                    <img className="ml-2 w-6 h-6" src={Chefs} alt="chefs" />
                    <img className="ml-2 w-6 h-6" src={Chefs} alt="chefs" />
                </div>
            </div>
            <div className='md:flex py-2 '>
                <p className="md:w-1/2">{categories}</p>
                <p className="md:-1/2 mt-1 text-black">{fitness}</p>
                {!hideprice &&
                    <div><p className='text-main ml-4 font-semibold'>{price}</p></div>}
            </div>
            <div className='md:flex py-2 '>
                <p className="md:w-1/2">{time}</p>
                <p className="md:w-1/2 text-main underline">{days}</p>
            </div>
            <div className='md:flex py-2 '>
                <p className="w-1/2">{ingredients}</p>
                <p className="w-1/2 text-black">{number}</p>
            </div>

        </div>
    )
}

export default Details

```
Cómo ejecución del código del resultado final es lo que se muestra en la imagen.

![](https://i.imgur.com/ICEzwHy.jpg)
 
[Subir](#top)


<a name="item38"></a>
### 

![]()
 
[Subir](#top)


<a name="item39"></a>
### Tab
 
Componente dinamico encargado del movimiento del cambio de las lista seleccionada.

Recibe como parámetro { children, value, onClick, canContinue = true } children es la variable que almacena el contenido de cada pestaña, value es el estilo de seleccion de la pestaña, onclick es la variable lógica para saber el click y el canContinue es el que me permite volver al estado original con valores lógico.

#### Código
```
import clsx from "clsx";
import { useTabs } from "../contexts/TabsContext";

const Tab = ({ children, value, onClick, canContinue = true }) => {
    const { value: contextValue, setValue } = useTabs();

    return <div
        className={clsx([
            'px-5 py-2 md:font-semibold font-medium md:text-lg text-sm cursor-pointer',
            { 'border-b-2 border-main': value === contextValue }
        ])}
        onClick={() => {
            if (canContinue) {
                setValue(value);
                onClick?.(value);
            }
        }}
    >
        {children}
    </div>;
};

export default Tab;
```
Cómo ejecución del código del resultado final es lo que se muestra en la imagen.

![](https://i.imgur.com/EjGCgq4.jpg)

[Subir](#top)



<a name="item41"></a>
### TabPanel
 
Componente encargado de mostar o ocultar la información de sus hijos dependiendo de la pestaña seleccionada.

Recibe como parámetro { children, className, value } children es la variable que almacena el contenido de cada pestaña, value es el estilo de selección de la pestaña, className es la clases en particular que tiene el cuerpo del contenido interno a mostrar.

#### Código
```
import { useTabs } from "../contexts/TabsContext";

const TabPanel = ({ children, className, value }) => {
    const { value: contextValue } = useTabs();

    if (value !== contextValue) return null;

    return <div className={className}>{children}</div>;
};

export default TabPanel;
```
Cómo ejecución del código del resultado final es lo que se muestra en la imagen.}

![](https://i.imgur.com/EjGCgq4.jpg)

[Subir](#top)







<a name="item42"></a>
### TabsContainer
 
chequea que sus hijos si es 1 lo muestra si son muchos lo rederiza.


![](https://i.imgur.com/XmcMSTW.jpg)
 
[Subir](#top)





<a name="item43"></a>
### TotalShopping
 
componente encargado de mostrar imagen de un tamaño en particular para la vista del producto


![](https://i.imgur.com/fUptzyn.jpg)

[Subir](#top)







<a name="item44"></a>
### TotalShoppingPrice
 
Componente  encargado de mostrar precio en la vista del detalle del producto unico

![](https://i.imgur.com/W5vbfBG.jpg)
 
[Subir](#top)





<a name="item45"></a>
### InformationChef
 
componente encargado de Mostrar las redes sociales de chef


![](https://i.imgur.com/7BfR5Ig.jpg)
 
[Subir](#top)







<a name="item46"></a>
### DescriptionPost
 
Componente encargado de mostra del detalle de la descripcion de post del blog


![](https://i.imgur.com/PNWKOmO.jpg)

[Subir](#top)





<a name="item47"></a>
### CalendarDay
 
Componente encargado de recibir el dia correspondiente del calendar


![](https://live.staticflickr.com/65535/52094212550_2251271785_m.jpg)
 
[Subir](#top)




<a name="item48"></a>
### calendar
 
Componente encargado del diseño del calendario 


![](https://i.imgur.com/pPh6blH.jpg)
 
[Subir](#top)





<a name="item49"></a>
### RequireAuth
 
Componente de autenticacion del login de usuario. Envuelve MyAccountLayou.


![](https://i.imgur.com/H2GSeFq.png) 
 
[Subir](#top)






<a name="item50"></a>
### ScrollNavegacion
 
Componente encargado de contener el diseño circular. Componente principal ButtonButton(ScrollNavegacion)


![](https://i.imgur.com/axBDP5H.png)

[Subir](#top)





<a name="item51"></a>
### SearchHome
 
Componente encargado de motor de Busqueda en el home contiene el componente ButtonSearch


![](https://i.imgur.com/VUipCHj.jpg)
 
[Subir](#top)



<a name="item52"></a>
* ### ButtonSearch
 
Componente encargado del selector de busqueda por sus categorias.


![](https://i.imgur.com/ZcvnIqL.jpg)

[Subir](#top)





<a name="item53"></a>
### WeightPlan
 
Componente de la vista de cuadro de planes. 

![](https://i.imgur.com/zz5z3jo.jpg)

[Subir](#top)







<a name="item54"></a>
### Swiper
 
CategoryCard, Combos, Home, Overview, Popular, Recipes, WeightPlan


![]()

[Subir](#top)





<a name="item55"></a>
### config
 
Componente de la parte del usuario en la vista de configuracion.


![](https://i.imgur.com/EABaJmL.png)

[Subir](#top)





<a name="item56"></a>
### DescriptionChef
 
Componente encargado del chef de la description del menu lateral


![](https://i.imgur.com/Z317Uop.jpg)
 
[Subir](#top)





<a name="item57"></a>
### DescriptionPost
 
Componente encargado de mostrar la informacion de post de Anya del menu lateral


![](https://i.imgur.com/lbnWbfI.jpg)

[Subir](#top)




<a name="item58"></a>
### FormAccount
 
Componente de la informacion personal de user en la vista de usuario (my personal informayion)


![](https://i.imgur.com/oBI4w4l.jpg)

[Subir](#top)





<a name="item59"></a>
### InformacionChef
 
Datos de los canales de venta del chef que aparece en el menu lateral.


![](https://i.imgur.com/KmzMHy8.jpg)

[Subir](#top)







<a name="item60"></a>
### ingredientRow
 
Componente encargado del diseño del cuadro de la lista de ingredientes.


![](https://i.imgur.com/NZWLwnL.jpg)
 
[Subir](#top)





<a name="item61"></a>
### ingredientRowDetails

Componente encargado del detalle que lleva cada vista de la lista de ingredientes.


![](https://i.imgur.com/NZWLwnL.jpg)

[Subir](#top)




<a name="item62"></a>
### LyOverview

Componente encargado del diseño de las letras de la vista overview


![](https://i.imgur.com/PwvSgsV.jpg)

[Subir](#top)




<a name="item63"></a>
### MealDetailOverview

componente del scroll de la vista por dia.


![]()

[Subir](#top)




<a name="item64"></a>
### MealDetailOverviewImages

Componete encargado de mostrar la imagenes al seleccionar un cuadro de la vista de overview.

![]()

[Subir](#top)




<a name="item65"></a>
### PasswordUser

Componente donde permite al usuario agregar contraseña en la vista paypal user.

![](https://i.imgur.com/R2OqFUW.png)
 
[Subir](#top)

<a name="item65"></a>
### PaypalLogin

Componente que fue creado para mostrar el diseño de PayPal de iniciar sesión de paypal.

![](https://i.imgur.com/Ohu20I5.png)
 
[Subir](#top)



<a name="item67"></a>
### PaypalUser

Componente que se encarga de colocar la informacion de my paypal en la vista de user.


![](https://i.imgur.com/Ua3GKRL.jpg)

[Subir](#top)




<a name="item68"></a>
### ProductInfo

Componente que se encarga mostrar todo el contenido de la vista de detalle del producto.

![](https://i.imgur.com/oaZUbKe.jpg)

[Subir](#top)




<a name="item69"></a>
### BannerPage

componente del banner de las diferente vista (revision).

![](https://i.imgur.com/aG1xRyc.png)

[Subir](#top)




<a name="item70"></a>
### BoxCalendar

Componente encargado del diseño del cuadro del calendario de la vista del usuario

![](https://i.imgur.com/9gQbIlN.jpg)

[Subir](#top)




<a name="item71"></a>
### BoxName

Componente que recibe el texto del dia de la semana (Sunday, Monday, Tuesday, Wednesday, Thursday, Friday).

![]()

[Subir](#top)




<a name="item72"></a>
### ButtonCart

Componente del boton de carrito.

![](https://i.imgur.com/xYF5GkZ.jpg)

[Subir](#top)




<a name="item73"></a>
### ButtonChange

Componente del boton de change

![](https://i.imgur.com/8FCip2e.png)

[Subir](#top)




<a name="item74"></a>
### ButtonItems

Componente que se encarga del diseño del boton de seleccion de (recipes, plans y combos)

![](https://i.imgur.com/O9JlBX9.png)

[Subir](#top)




<a name="item75"></a>
### SelectOrder

Componente del diseño de lista de ordenar por del vendedor.	

![](https://i.imgur.com/Q31CQTS.png)

[Subir](#top)




<a name="item76"></a>
### CardChef

Componente del vendedor. Vista sellers.

![](https://i.imgur.com/s4rgz6r.jpg)

[Subir](#top)





<a name="item78"></a>
### CardOrder

Componente donde aparece foto de nombre del vendedor, order, sellers.

![](https://i.imgur.com/IDxf85y.png)

[Subir](#top)




<a name="item79"></a>
### CardPaypal

Componente que se encuentra en la vista de la forma de pago de paypal (logo y modificar).

![](https://i.imgur.com/HYISllZ.png)

[Subir](#top)




<a name="item80"></a>
### CardProduct

Componente que contiene imagen y titulo del producto en la vista de paypal.

![](https://i.imgur.com/fgykcjx.png)

[Subir](#top)




<a name="item81"></a>
### CardRecipes

Componente de las recetas. 

![](https://i.imgur.com/eJSBoxj.png)

[Subir](#top)




<a name="item82"></a>
### CardResum

Componente de orden de resum en paypal.

![](https://i.imgur.com/3fKcpYB.jpg)

[Subir](#top)




<a name="item83"></a>
### CardWithTitle

Componente que fue realizado para la parte de configuraciones de My servings en la vista de usuario.

![](https://i.imgur.com/wv1BuLk.jpg)

[Subir](#top)






<a name="item84"></a>
### Checkbox

Componente del checkbok cuadrado.

![](https://i.imgur.com/D2ZuNwI.jpg)

[Subir](#top)




<a name="item85"></a>
### CheckboxConfig

Componente del checkbok circular.

![](https://i.imgur.com/tBic1Xs.jpg)

[Subir](#top)




<a name="item86"></a>
### WaPay

Componente encargado de mostrar la informacion de la lista de comparador de precio

![](https://i.imgur.com/tvnn47v.png)

[Subir](#top)


